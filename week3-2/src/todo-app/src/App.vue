<script setup>
import { reactive, ref } from 'vue'

// const todoList = ref([])
const todoObjList = reactive([
  { text: '할 일 1', checked: false, isEditing: false },
  { text: '할 일 2', checked: false, isEditing: false },
])
const newTodoItem = ref('')

function addTodoList() {
  todoObjList.push({ text: newTodoItem.value, checked: false, isEditing: false })
  newTodoItem.value = ''
}

function completeTodoClass(item) {
  return item.checked ? 'line-through' : ''
}

function deleteTodo(index) {
  todoObjList.splice(index, 1)
}
// TODO 목록 리스트를 만들어서, 입력창에다가 입력하고 '등록' 버튼을 누르면 변수에 추가가 되도록 만들어보기
</script>
<template>
  <h1 class="text-3xl font-bold underline">Hello world!</h1>

  <p>
    Visit <a href="https://vuejs.org/" target="_blank" rel="noopener">vuejs.org</a> to read the
    documentation
  </p>

  <div>
    <InputText v-model="newTodoItem" @keyup.enter="addTodoList" />
    <Button @click="addTodoList">등록</Button>
  </div>

  <div>
    <ul>
      <li v-for="(item, index) in todoObjList" :key="index">
        <div class="flex items-center gap-2">
          <!-- <span :class="{ 'line-through': item.checked }">{{ item.text }}</span> -->
          <!-- <span :style="{ 'text-decoration-line': `${item.checked} ? 'line-through' : ''` }">{{item.text}}</span>-->
          <span v-if="!item.isEditing">
            <ToggleSwitch v-model="item.checked" />
            <span :class="completeTodoClass(item)">{{ item.text }}</span>
            <button @click="item.isEditing = true">
              <i class="pi pi-pencil" style="font-size: 2rem"></i>
            </button>
            <button @click="deleteTodo(index)">
              <i class="pi pi-trash" style="font-size: 2rem"></i>
            </button>
          </span>
          <span v-else>
            <InputText v-model="item.text" @keyup.enter="item.isEditing = false" />
            <Button @click="item.isEditing = false">수정</Button>
            <!-- <Button @click="item.isEditing = false">취소</Button> -->
          </span>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
