<script setup>
import { ref, computed } from 'vue';
import TodoItem from './TodoItem.vue';

const props = defineProps({
  todos: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(['remove-todo']);

// 篩選出 已完成 待完成 功能
// 預設是 all 代表顯示全部待辦的狀態
// 三個 a tag 綁定ref點擊事件 如果點擊狀態字串就更改
// class active 也要綁定 v-bind 如果filterStatus內的字串變成相對應的字串就顯示active class
const filterStatus = ref('all');
const filterTodos = computed(() => {
  // 第一個參數代表依照什麼條件去做不同的事情
  // 如果case是什麼就回傳什麼
  // 在將篩選好的放到v-for的資料
  switch (filterStatus.value) {
    case 'incomplete':
      return props.todos.filter((t) => !t.status);
    case 'complete':
      return props.todos.filter((t) => t.status);
    default:
      return props.todos;
  }
});

// 顯示未完成項目數量 功能
// 篩選出status為false的資料
// 在 未完成項目 html上 顯示篩選後的資料幾筆 length
const incompleteTodos = computed(() => props.todos.filter((t) => !t.status));
</script>

<template>
  <div class="todoList_list">
    <ul class="todoList_tab">
      <li>
        <a
          href="#"
          @click.prevent="filterStatus = 'all'"
          :class="{ active: filterStatus === 'all' }"
          >全部</a
        >
      </li>
      <li>
        <a
          href="#"
          @click.prevent="filterStatus = 'incomplete'"
          :class="{ active: filterStatus === 'incomplete' }"
          >待完成</a
        >
      </li>
      <li>
        <a
          href="#"
          @click.prevent="filterStatus = 'complete'"
          :class="{ active: filterStatus === 'complete' }"
          >已完成</a
        >
      </li>
    </ul>
    <div class="todoList_items">
      <ul class="todoList_item">
        <!-- 將todos的資料使用v-for遍歷出來 然後再props給孫子層 -->
        <!-- @remove-todo="emit('remove-todo', $event)" -->
        <!-- $event 代表的是「事件物件」或是子元件傳出的資料 意思是從子元件傳到子孫件 -->
        <TodoItem
          v-for="todo in filterTodos"
          :key="todo.id"
          :todo="todo"
          @remove-todo="emit('remove-todo', $event)"
        />
      </ul>
      <div class="todoList_statistics">
        <p>{{ incompleteTodos.length }} 個未完成項目</p>
      </div>
    </div>
  </div>
</template>
