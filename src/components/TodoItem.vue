<script setup>
const props = defineProps({
  todo: {
    // 因為單一是物件所以使用物件格式
    type: Object,
    required: true,
  },
});

const emit = defineEmits(['remove-todo']);
const handleRemoveTodo = (id) => {
  emit('remove-todo', id);
};
</script>

<template>
  <li>
    <label class="todoList_label">
      <!-- 雙向綁定v-model讓status顯示 true false -->
      <input class="todoList_input" type="checkbox" value="true" v-model="todo.status" />
      <span>{{ todo.content }}</span>
    </label>
    <a href="#" @click.prevent="handleRemoveTodo(todo.id)">
      <i class="fa fa-times"></i>
    </a>
  </li>
</template>
