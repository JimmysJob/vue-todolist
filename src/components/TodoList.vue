<script setup>
import TodoItem from './TodoItem.vue';

const props = defineProps({
  todos: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(['remove-todo']);
</script>

<template>
  <div class="todoList_list">
    <ul class="todoList_tab">
      <li><a href="#" class="active">全部</a></li>
      <li><a href="#">待完成</a></li>
      <li><a href="#">已完成</a></li>
    </ul>
    <div class="todoList_items">
      <ul class="todoList_item">
        <!-- 將todos的資料使用v-for遍歷出來 然後再props給孫子層 -->
        <!-- @remove-todo="emit('remove-todo', $event)" -->
        <!-- $event 代表的是「事件物件」或是子元件傳出的資料 意思是從子元件傳到子孫件 -->
        <TodoItem
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          @remove-todo="emit('remove-todo', $event)"
        />
      </ul>
      <div class="todoList_statistics">
        <p>5 個已完成項目</p>
      </div>
    </div>
  </div>
</template>
