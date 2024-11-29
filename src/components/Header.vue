<template>
  <el-page-header class="header">
    <template #content>
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/' }" class="breadcrumb">Сценарии</el-breadcrumb-item>
        <el-breadcrumb-item>
          Новый сценарий
        </el-breadcrumb-item>
      </el-breadcrumb>
    </template>
    <template #extra>
      <div class="flex items-center">
        <el-switch
            v-model="value2"
            class="ml-2"
            style="--el-switch-on-color: #67C23A; --el-switch-off-color: #909399"
            active-text="Сценарий запущен"
        />
        <el-button>История запусков</el-button>
        <el-button class="save-btn">Сохранить
          <el-icon><Select/></el-icon>
        </el-button>
      </div>
    </template>
  </el-page-header>
</template>
<script setup>
import {ref} from 'vue'
import {Select} from '@element-plus/icons-vue'

const value2 = ref(true)
</script>

<style>
.el-header {
  padding: 19px 30px !important;
  border-bottom: 1px solid #DCDFE6;
}

.el-header .el-page-header__back,
.el-header .el-divider {
  display: none !important;
}

.save-btn {
  background-color: #844CE6 !important;
  font-family: Roboto;
  color: #FFFFFF !important;
}

.el-breadcrumb__inner.is-link {
  color: #303133 !important;
//font-family: PingFang SC;
}


.el-breadcrumb__inner.is-link, .save-btn {
  font-size: 14px;
  font-weight: 500 !important;
  line-height: 22px;
}

.el-breadcrumb__inner {
  color: #909399 !important;
  font-size: 14px;
  line-height: 22px;
}

.el-switch {
  flex-direction: row-reverse;
  margin-right: 12px;
}

.el-switch__label--right {
  margin-right: 8px;
  color: #303133 !important;
  opacity: 0.5;
  font-size: 13px;
  font-weight: 400;
  line-height: 22px;
}

.el-switch__label.is-active {
  opacity: 1;
}
</style>