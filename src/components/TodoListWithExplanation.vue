<template>
  <main
    class="d-flex flex-column justify-center"
    style="height: 10rem"
  >
    <h1 style="margin-bottom: 1rem; text-align: center">
      TodoList
    </h1>
    <div class="d-flex ga-4 align-center">
      <v-text-field
        label="輸入待辦事項"
        variant="outlined"
        width="300px"
        v-model="tempTodo"
      />
      <v-btn @click="addTodo" variant="tonal">add</v-btn>
    </div>
    <div
      v-for="item in todoItems"
      :key="item.id"
      class="d-flex align-center ga-8"
    >
      <v-checkbox
        :key="item.id"
        color="primary"
        :label="item.todo"
        v-model="item.status"
        v-if="item.status != null"
      >
      </v-checkbox>
      <v-icon
        icon="mdi-delete"
        style="margin-bottom: 1rem"
        v-if="item.status != null"
        @click="removeTodo(item.id)"
      />
    </div>
  </main>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue'

const tempTodo = ref('')

// 在這個情境下用 interface 跟 type 都可以
// 介面: 定義物件的型別，對「物件的形狀（Shape）」進行描述
// interface ITodoItem {
//   todo: string
//   id: string
//   status: boolean | null
// }

// 型別別名: 用 type 關鍵字定義
type ITodoItem = {
  todo: string
  id: string
  status: boolean | null
}

// 型別推論: TypeScript 幫你推論出型別
// const todoItems = reactive([
// 型別斷言: 陣列泛型寫法
// const todoItems: Array<ITodoItem> = reactive([
// 型別斷言: 大括號陣列寫法
// const todoItems: ITodoItem[] = reactive([
// 型別斷言: 再另一種寫法
// const todoItems = reactive<ITodoItem[]>([
// 型別註記: 用冒號註記
const todoItems: {
  todo: string
  id: string
  status: boolean | null
}[] = reactive([
  {
    todo: 'Git',
    id: '1',
    status: false
  },
  {
    todo: 'JavaScript',
    id: '2',
    status: false
  },
  {
    todo: 'TypeScript',
    id: '3',
    status: false
  }
])

// void 關鍵字：讓 TypeScript 知道該 function 沒有回傳值
const addTodo = (): void => {
  if (tempTodo.value === '') return
  todoItems.push({
    todo: tempTodo.value,
    id: new Date().toString(),
    status: false
  })
  tempTodo.value = ''
}

// 型別別名: 用 type 關鍵字定義 ()=>{} 型別
// p.s. 我不會先用 type 定義，基本上都直接註記
type FRemoveTodo = (id: string) => void

const removeTodo: FRemoveTodo = (id) => {
  // 型別註記
  // const removeTodo = (id: string): void => {
  todoItems.filter((item) => item.id === id)[0].status =
    null
}
</script>
