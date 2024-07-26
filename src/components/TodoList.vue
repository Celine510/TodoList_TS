<template>
  <main class="d-flex flex-column justify-center">
    <h1 style="margin-bottom: 2rem; text-align: center">
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

interface ITodoItem {
  todo: string
  id: string
  status: boolean | null
}

const todoItems: ITodoItem[] = reactive([
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

const addTodo = (): void => {
  if (tempTodo.value === '') return
  todoItems.push({
    todo: tempTodo.value,
    id: new Date().toString(),
    status: false
  })
  tempTodo.value = ''
}

const removeTodo = (id: string): void => {
  todoItems.filter((item) => item.id === id)[0].status =
    null
}
</script>
