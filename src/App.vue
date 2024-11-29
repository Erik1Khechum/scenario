<script setup>
import LeftMenu from "@/components/LeftMenu.vue";
import Scenario from "@/views/Scenario.vue";
import Header from "@/components/Header.vue";
</script>

<template>
  <div class="common-layout">
    <el-container>
      <el-aside width="389px">
        <LeftMenu/>
      </el-aside>
      <el-container>
        <el-header>
          <Header/>
        </el-header>
        <el-main class="main">
          <Scenario/>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<style>
.main{
  padding: 0;
  height: calc(100vh - 78px);
}
</style>
