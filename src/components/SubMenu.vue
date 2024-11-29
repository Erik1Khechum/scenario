<template>
  <div class="sub-menu">
    <div>
      <el-form :model="form" label-width="auto" class="search-form">
        <el-form-item class="search-box">
          <el-input
              v-model="form.search"
              style="width: 284px"
              size="large"
              placeholder="Поиск"
              :prefix-icon="Search"
          />
        </el-form-item>
      </el-form>
      <el-menu
          default-active="2"
      >
        <template v-for="(item, index) in subMenu">
          <el-menu-item :index="index" v-if="!item.items" :class="{active: index === 2}">
            <el-row style="width: 100%">
              <el-col :span="22">
                <el-row>
                  <el-col :span="3">
                    <el-icon>
                      <component :is="item.icon"/>
                    </el-icon>
                  </el-col>
                  <el-col :span="21">
                    <p>{{ item.name }}</p>
                    <span :class="['status', { green: item.status === 1 }] ">{{ item.status_name }}</span>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="2">
                <el-icon class="more-icon">
                  <More/>
                </el-icon>
              </el-col>
            </el-row>

          </el-menu-item>
          <el-sub-menu :index="index" v-else>
            <template #title>
              <el-icon>
                <component :is="item.icon"/>
              </el-icon>
              <span>{{ item.name }}</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="1-1">item one</el-menu-item>
              <el-menu-item index="1-2">item two</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
        </template>
      </el-menu>
    </div>

    <div class="p-4 sub-menu-btn-box">
      <el-button :icon="Plus" class="new-scenario-btn btn" size="large">Новый сценарий</el-button>
      <el-button class="add-folder-btn" :icon="FolderAdd" size="large"></el-button>
    </div>

  </div>
</template>
<script setup>
import {ref} from 'vue'
import {Search} from '@element-plus/icons-vue'
import {reactive} from 'vue'
import {
  Folder,
  VideoPlay,
  More,
  Plus,
  FolderAdd
} from '@element-plus/icons-vue'

const search = ref('')
const subMenu = ref([
  {
    'icon': ref(VideoPlay),
    'name': 'Telegram-бот',
    'status_name': 'Запущен',
    'status': 1,
    'items': false,

  },
  {
    'icon': ref(Folder),
    'name': 'Сайт',
    'status_name': '4 сценария',
    'status': 2,
    'items': true,
  },
  {
    'icon': ref(VideoPlay),
    'name': 'Новый сценарий',
    'status_name': 'Запущен',
    'status': 1,
    'items': false,
  },
  {
    'icon': ref(VideoPlay),
    'name': 'Регистрация',
    'status_name': 'Остановлен',
    'status': 0,
    'items': false,
  },
  {
    'icon': ref(VideoPlay),
    'name': 'API: Список объявлений',
    'status_name': 'Запущен',
    'status': 1,
    'items': false,
  }
]);


const form = reactive({
  search: '',
})


</script>
<style>
.sub-menu {
  border-right: 1px solid #DCDFE6;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.sub-menu .el-menu {
  border-right: 0 !important;
}

.search-form {
  padding: 19px 18px;
}

.search-box{
  margin-bottom: 0 !important;
}

.sub-menu .el-menu-item {
  height: auto !important;
  line-height: normal !important;
  width: 100%;
  padding: 4px 18px !important;
}

.sub-menu .el-menu-item.active,
.sub-menu .el-menu-item:hover,
.sub-menu .el-sub-menu.active,
.sub-menu .el-sub-menu:hover
{
  background-color: #F4F0FF !important;
}

.sub-menu svg path {
  fill: #606266;
}

.sub-menu p {
  font-family: PingFang SC;
  font-size: 14px;
  font-weight: 500;
  line-height: 23px;
  color: #303133;
}

.status {
  font-family: PingFang SC;
  font-size: 12px;
  font-weight: 400;
  line-height: 20px;
  color: #909399;
}

.green {
  color: #67C23A;
}

.more-icon svg path {
  fill: #B1B5BE;
}

.p-4 {
  padding: 16px;
}

.sub-menu-btn-box .el-button + .el-button {
  margin-left: 8px !important;
}


.new-scenario-btn {
  max-width: 240px;
  width: 100%;
}

.add-folder-btn {
  width: 40px;
}

.btn{
  font-family: Roboto;
  font-size: 14px;
  font-weight: 500;
  line-height: 22px;
}
</style>