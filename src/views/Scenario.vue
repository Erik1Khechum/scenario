<template>
  <el-row>
    <el-col :span="17">

      <div class="flex justify-between">

        <NestedDraggable v-model="list" group="action" class="w-full"></NestedDraggable>
        <preview-list :list="list" />
      </div>


    </el-col>

    <el-col :span="7" class="action-block">
      <h2 class="title">Добавить действие</h2>
      <div v-for="(group, type) in groupedActions" :key="type" class="action-card">
        <h3 class="subtitle">{{ group[0].typeName }}</h3> <!-- Display typeName for the group -->

        <VueDraggable
            v-model="actions"
            :animation="150"
            :group="{ name: 'action', pull: 'clone', put: false }"
            :sort="false"
            class="action-group"
            @clone="onClone"
        >
          <div
              v-for="item in group"
              :key="item.id"
              class="action-list-item"
              :data-id="item.id"
          >
            <img :src="item.icon" alt="" width="20" height="20"/>
            <span>{{ item.id + item.name }}</span>
          </div>
        </VueDraggable>
      </div>

    </el-col>

  </el-row>
</template>

<script setup>
import { ref, computed } from 'vue';
import {VueDraggable} from 'vue-draggable-plus'
import NestedDraggable from "@/components/NestedDraggable.vue";

const actions = ref([
  {
    id: '1',
    name: 'Создать запись',
    icon: 'static/icons/actions/data.svg',
    content: 'В таблице Администраторы',
    type: '1',
    typeName: 'База данных',
    badge: 'newRecord',
  },
  {
    id: '2',
    name: 'Обновить записи',
    icon: 'static/icons/actions/data-update.svg',
    content: '',
    type: '1',
    typeName: 'База данных',
    badge: 'updateRecords'
  },
  {
    id: '3',
    name: 'Найти запись',
    icon: 'static/icons/actions/data-find.svg',
    content: 'В таблице Администраторы',
    type: '1',
    typeName: 'База данных',
    badge: 'searchRecords'
  },
  {
    id: '4',
    name: 'Удалить запись',
    icon: 'static/icons/actions/data-delete.svg',
    content: '',
    type: '1',
    typeName: 'База данных',
    badge: 'deleteRecords'
  },
  {
    id: '5',
    name: 'Если',
    icon: 'static/icons/actions/frame.svg',
    content: '{{form.field_by_id = “Регистрация”}}',
    type: '2',
    typeName: 'Условия и действия',
    badge: ''
  },
  {
    id: '6',
    name: 'Иначе',
    icon: 'static/icons/actions/frame.svg',
    content: '{{form.field_by_id = “Новый администратор”}}',
    type: '2',
    typeName: 'Условия и действия',
    badge: ''
  },
  {
    id: '7',
    name: 'HTTP-запрос',
    icon: 'static/icons/actions/earth.svg',
    content: 'https://hook.creatium.io/25gsf1ph594rnktv2cdtxum5ucjpav5f',
    type: '2',
    typeName: 'Условия и действия',
    badge: 'http'
  },
  {
    id: '8',
    name: 'Таймер',
    icon: 'static/icons/actions/clock.svg',
    content: '5 секунд',
    type: '2',
    typeName: 'Условия и действия',
    badge: 'timer'
  },
  {
    id: '9',
    name: 'Выполнить код',
    icon: 'static/icons/actions/code.svg',
    content: '',
    type: '2',
    typeName: 'Условия и действия',
    badge: ''
  },
  {
    id: '10',
    name: 'Создать пользователя',
    icon: 'static/icons/actions/add-user.svg',
    content: '',
    type: '3',
    typeName: 'newUser',
    badge: ''
  },
  {
    id: '11',
    name: 'Изменить почту',
    icon: 'static/icons/actions/edit-email.svg',
    content: '',
    type: '3',
    typeName: 'Пользователи',
    badge: ''
  },
  {
    id: '12',
    name: 'Восстановить пароль',
    icon: 'static/icons/actions/recover-pass.svg',
    content: '',
    type: '3',
    typeName: 'Пользователи',
    badge: ''
  }
])


const list = ref(
    actions.value.map(item => ({
      ...item,
      name: `${item.name}`,
      id: `${item.id}`,
    }))
);

function onClone(evt) {
  const clonedItem = evt.item;
  const originalItemId = clonedItem.dataset.id;
  const originalItem = actions.value.find(action => action.id === originalItemId);
  if (originalItem) {
    const clonedAction = {
      ...originalItem,
      name: `${originalItem.name}`
    };
    list.value.push(clonedAction);
  }
}




const groupedActions = computed(() => {
  return actions.value.reduce((groups, action) => {
    if (!groups[action.type]) {
      groups[action.type] = [];
    }
    groups[action.type].push(action);
    return groups;
  }, {});
});
</script>

<style scoped>
.action-block{
  border-left: 1px solid #DCDFE6;
}
.title {
  font-family: Rubik;
  font-size: 16px;
  font-weight: 500;
  line-height: 23px;
  color: #303133;
  padding: 24px 20px 17px;
}
.action-card{
  padding: 12px 20px;
  border-bottom: 1px solid #DCDFE6;
}

.subtitle {
  font-family: Rubik;
  font-size: 14px;
  font-weight: 500;
  line-height: 23px;
  color: #303133;
  margin-bottom: 12px;
}

.action-list-item {
  background: #F5F7FA;
  height: 48px;
  padding: 8px;
  display: flex;
  align-items: center;
  cursor: pointer;
}

.action-list-item:not(:last-child) {
  margin-bottom: 8px;
}

.action-list-item img {
  margin-right: 10px;
}

.action-list-item span {
  font-family: Rubik;
  font-size: 14px;
  font-weight: 400;
  line-height: 23px;
  color: #303133;
}

</style>
