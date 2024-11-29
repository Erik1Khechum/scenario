<template>
  <el-row>
    <el-col :span="4">
      <el-menu
          default-active="2"
          class="left-menu"
          :collapse="false"
      >
        <el-menu-item index="1">
          <img :src="logo" alt="Logo" width="32px" height="32px" class="logo"/>
        </el-menu-item>

        <el-menu-item-group v-for="(item, index) in menu" :key="index">
          <template #title>
            <span class="menu-title">{{ item.name }}</span>
          </template>
          <el-menu-item
              v-for="(subItem, subIndex) in item.items"
              :key="subIndex"
              :index="`${index}-${subIndex}`"
          >
        <span class="icon-box">
                  <img :src="subItem.icon" alt="Sub-item icon" class="icon" width="18px" height="18px"/>

        </span>
          </el-menu-item>
        </el-menu-item-group>
      </el-menu>
    </el-col>
    <el-col :span="20">
      <SubMenu/>
    </el-col>
  </el-row>
</template>

<script setup>
import {ref} from 'vue'
import SubMenu from './SubMenu.vue';
import {
  Document,
  Menu as IconMenu,
  Location,
  Setting,
} from '@element-plus/icons-vue'


const menu = ref([
  {
    "name": "Сайт",
    "items": [
      {
        "icon": "static/icons/LeftMenu/memo.svg",
        "items": []
      },
      {
        "icon": "static/icons/LeftMenu/plugin.svg",
        "items": []
      },
      {
        "icon": "static/icons/LeftMenu/setting.svg",
        "items": []
      }
    ]
  },
  {
    "name": "Данные",
    "items": [
      {
        "icon": "static/icons/LeftMenu/coin.svg",
        "items": []
      },
      {
        "icon": "static/icons/LeftMenu/folder.svg",
        "items": []
      },
    ]
  },
  {
    "name": "Логика",
    "items": [
      {
        "icon": "static/icons/LeftMenu/play.svg",
        "items": []
      },
      {
        "icon": "static/icons/LeftMenu/connection.svg",
        "items": []
      },
      {
        "icon": "static/icons/LeftMenu/calendar.svg",
        "items": []
      },
    ]
  },
]);

const logo = "static/icons/LeftMenu/logo.svg";
</script>

<style>
.left-menu {
  //width: 70px;
  height: 100vh;
  border-right: 1px solid #DCDFE6;
  padding: 23px 4px;
}

.left-menu .el-menu-item-group:not(:last-child) {
  border-bottom: 1px solid #DCDFE6;
  margin: 16px 0;
}

.left-menu ul {
  padding: 8px 0 !important;
}

.el-menu-item {
  padding: 0 !important;
  height: fit-content !important;
}

.el-menu-item:hover {
  background-color: transparent !important;
}

.el-menu-item:hover .icon-box {
  background-color: #F4F0FF;
}

.icon-box {
  line-height: normal;
  padding: 13px;
  margin: 0 auto;
}


.icon {
  margin: 0 auto;
}

.logo {
  margin: 0 auto 16px;
}

.el-menu-item-group__title {
  padding: 0 !important;
  text-align: center;
}
</style>