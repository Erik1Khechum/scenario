<template>
  <el-row class="drag-area-item">
    <el-col :span="2" class="drag-area-column">
      <div class="img-box">
        <img :src="polygon" alt="icon"/>
        <div class="vertical-line"> </div>
      </div>
    </el-col>
    <el-col :span="22" class="content-box">
      <div class="content-box-name">
        <p>Запуск сценария</p>
        <span>input</span>
      </div>
    </el-col>
  </el-row>
  <ul class="drag-area" ref="el">
    <li v-for="el in modelValue" :key="el.name">
      <el-row class="drag-area-item">
        <el-col :span="2">
          <div class="img-box">
            <img :src="el.icon" alt="icon"/>
          </div>
        </el-col>
        <el-col :span="22" class="content-box">
          <div class="content-box-name">
            <p>{{ el.name }}</p>
            <span class="">{{ el.badge }}</span>
          </div>
          <span>{{ el.content }}</span>
        </el-col>
      </el-row>
            <NestedDraggable v-if="el.children && el.children.length > 0" v-model="el.children" />
    </li>
  </ul>
</template>

<script setup lang="ts">
import {useDraggable} from 'vue-draggable-plus'
import {computed, ref} from 'vue'
import NestedDraggable from '@/components/NestedDraggable.vue' // Не забудьте импортировать компонент


const polygon = 'static/icons/actions/polygon.svg'
interface IList {
  name: string
  content: string
  icon: string
  badge: string
  children?: IList[]
}

interface Props {
  modelValue: IList[]
}

const props = defineProps<Props>()

interface Emits {
  (e: 'update:modelValue', value: IList[]): void
}

const emits = defineEmits<Emits>()

const list = computed({
  get: () => props.modelValue,
  set: value => emits('update:modelValue', value)
})

const el = ref()
useDraggable(el, list, {
  group: 'g1'
})
</script>

<style scoped>
.drag-area {
  //min-height: 50px;
}
.drag-area-item{
  display: flex;
  align-items: center;
  margin: 20px 0;
}
.drag-area li {
  list-style: none;
}

.img-box {
  border: 1px solid #CDD0D6;
  width: 45px;
  height: 45px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.content-box {
  padding-left: 6px;
}

.content-box-name{
  display: flex;
  align-items: center;
}
.content-box-name p {
  font-size: 14px;
  font-weight: 500;
  line-height: 23px;
  color: #303133;
}
.content-box-name span{
  padding: 1px 6px;
  border-radius: 9px;
  background: #E8E0FC;
  border: 1px solid #FFFFFF;
  color: #8B63EF !important;
  margin-left: 12px;
}
.content-box span{
  font-family: Rubik;
  font-size: 12px;
  font-weight: 400;
  line-height: 16px;
  color: #909399;
}

.vertical-line {
  position: absolute;
  width: 1px;
  height: 100%;
  background-color: #CDD0D6;
  top: 45px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 0;
}


</style>
