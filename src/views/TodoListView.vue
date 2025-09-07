<script setup>
import TodoForm from '@/components/TodoForm.vue';
import TodoList from '@/components/TodoList.vue';
import { ref } from 'vue';

// 新增 todo 功能 todo 會有多筆資料所以使用 []
// 資料結構為 id 待辦內容content 是否完成待辦status
// 要將此資料 props 給 TodoList and TodoItem 元件
const todos = ref([
  { id: 1, content: '把冰箱發霉的檸檬拿去丟', status: false },
  { id: 2, content: '打電話叫媽媽匯款給我', status: true },
]);

// addTodo 新增功能

const addTodo = (content) => {
  // 如果傳進來的content資料不等於空字串是有內容的就新增物件到todos
  if (content.trim() !== '') {
    todos.value.push({
      id: Date.now(),
      content: content,
      status: false,
    });
  }
};

// removeTodo 刪除功能
// 以todos的id來判定資料並且篩選出不等於傳入id的資料
// 使用emit的方式將@remove-todo函式帶入子元件Todolist
// 子元件defineEmits(['remove-todo'])接收'remove-todo'
// 然後再emit給子孫件@remove-todo="emit('remove-todo', $event)"
// 子孫件設定 handleRemoveTodo 點擊事件把資料傳到 Todolist 然後再傳回父元件
const removeTodo = (id) => {
  todos.value = todos.value.filter((t) => t.id !== id);
};
</script>

<template>
  <div id="todoListPage" class="bg-half">
    <nav>
      <h1><a href="#">ONLINE TODO LIST</a></h1>
      <ul>
        <li class="todo_sm">
          <a href="#"><span>王小明的代辦</span></a>
        </li>
        <li><a href="#loginPage">登出</a></li>
      </ul>
    </nav>
    <div class="conatiner todoListPage vhContainer">
      <div class="todoList_Content">
        <TodoForm @add-todo="addTodo" />
        <!-- 尚無待辦功能 : 如果todos內有資料才會顯示TodoList元件內容 -->
        <!-- 沒有資料的話就顯示 <p v-else>尚無待辦事項</p> -->
        <TodoList v-if="todos.length" :todos="todos" @remove-todo="removeTodo" />
        <p v-else>尚無待辦事項</p>
      </div>
    </div>
  </div>
</template>
