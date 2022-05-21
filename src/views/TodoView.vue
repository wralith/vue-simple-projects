<script setup lang="ts">
import { computed, onUpdated, ref } from 'vue'

interface todoItem {
  id: number
  name: string
  isDone: boolean
}

let todoList = ref<todoItem[]>([])
let todoInLocalStorage = window.localStorage.getItem('todos') || ''

// Get data from local storage if it exists
if (window.localStorage.getItem('todos') !== null) {
  todoList.value = JSON.parse(todoInLocalStorage)
}

// Save to local storage when component updated??
onUpdated(() => {
  window.localStorage.setItem('todos', JSON.stringify(todoList.value))
})

function deleteItem(item: object) {
  todoList.value = todoList.value.filter((t) => t != item)
}

let itemToAdd = ref('')
function addItem(item: string) {
  const uniqueId = Date.now()
  todoList.value = [...todoList.value, { id: uniqueId, name: item, isDone: false }]
  itemToAdd.value = ''
}

const todoLeft = computed(() => {
  let result = 0
  todoList.value.forEach((item) => (!item.isDone ? result++ : null))
  return result
})
</script>

<template>
  <main>
    <h1>Todo List</h1>

    <div class="todo-list">
      <ul>
        <h4 v-if="todoList.length < 1">
          Welcome! You can add TODO's either clicking <span>'add'</span> or pressing
          <span>'enter'</span>.
        </h4>
        <li v-for="item in todoList" :key="item.id">
          <div class="todo-item">
            <input type="checkbox" v-model="item.isDone" />
            <span :class="{ checked: item.isDone }">{{ item.name }}</span>
          </div>
          <small @click="deleteItem(item)">Delete</small>
        </li>
      </ul>
      <div class="todo-input">
        <a @click="addItem(itemToAdd)">Add</a>
        <input
          @keydown.enter="addItem(itemToAdd)"
          v-model="itemToAdd"
          type="text"
          placeholder="Todo"
        />
      </div>
      <p v-if="todoLeft > 0" class="todo-length-label">There is {{ todoLeft }} TODO's left.</p>
      <p v-if="todoLeft == 0" class="todo-length-label">There is no TODO at the moment.</p>
    </div>
  </main>
</template>

<style scoped lang="scss">
main {
  text-align: center;
  h4 span {
    color: $primary;
  }
}
.todo-list {
  position: relative;
  max-width: 60%;
  padding: 3rem 1rem 1rem;
  margin: auto;
  border-radius: 0.5rem;
  box-shadow: 0 0 5px rgb(39, 39, 39);

  @media (max-width: 720px) {
    max-width: 90%;
  }
}

ul {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  align-items: left;
  margin: 1rem auto;
  width: 100%;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  padding: 0.3rem;
  border: 1px solid darken($neutral-gray, 5%);
  input[type='checkbox'] {
    accent-color: $primary;
  }
  .todo-item {
    display: flex;
    flex-direction: row;
    text-align: left;
  }
}

.todo-input {
  margin-top: 3rem;
  display: flex;
  input {
    width: 100%;
    background-color: $light;
    border: none;
    transition: all ease 300ms;
    &:focus {
      outline: 3px solid $primary;
      border-radius: 0.5rem;
      background-color: white;
    }
  }
}

small,
a {
  background-color: #444;
  color: $primary;
  padding: 0.3rem;
  &:hover {
    background-color: $primary;
    color: $neutral-gray;
    cursor: pointer;
  }
  &:active {
    background-color: darken($primary, 10%);
  }
}

.checked {
  text-decoration: line-through;
  color: $primary;
}

.todo-length-label {
  text-align: right;
}
</style>
