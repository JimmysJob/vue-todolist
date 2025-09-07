<!-- 將輸入待辦事項拆解成元件 -->
<script setup>
import { ref } from 'vue';

const emit = defineEmits(['add-todo']);

const newTodo = ref('');

const handleAddTodo = (content) => {
  emit('add-todo', content);
  newTodo.value = '';
};
</script>

<template>
  <div class="inputBox">
    <input type="text" placeholder="請輸入待辦事項" v-model="newTodo" />
    <a href="#" @click.prevent="handleAddTodo(newTodo)">
      <i class="fa fa-plus"></i>
    </a>
  </div>
</template>
