<template>
  <div class="tasks-container">
    <Spinner v-if="!loaded" size="5rem" />
    <table v-if="loaded" class="fade-in">
      <tbody>
        <tr v-for="(todo, index) in todos" :key="todo.name">
          <td style="display:flex;">
            <span style="flex-grow: 1;">{{ todo.name }}</span>

            <input v-model="todo.isComplete" type="checkbox" @change="save()">
            <a class="btn btn-danger" @click="remove(index)">✘</a>
          </td>
        </tr>
        <tr>
          <td>
            <form style="display: flex;" @submit.prevent="add">
              <input v-model="newTodoName" style="flex-grow: 1; margin-right: 1rem;" type="text" placeholder="new todo">
              <button type="submit" :disabled="saving">
                ↑
              </button>
            </form>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Component } from 'vue-property-decorator'
import Spinner from './Spinner.vue'

@Component({
  components: {
    Spinner
  }
})
export default class Tasks extends Vue {
  static readonly localStorageKey = 'todos';

  loaded = false;
  saving = false;
  todos: { name: string; isComplete: boolean }[] = [];

  newTodoName = '';

  mounted () {
    const todosJson = localStorage.getItem(Tasks.localStorageKey)
    this.todos = JSON.parse(todosJson || '[]')

    this.loaded = true
  }

  add () {
    if (!this.newTodoName) {
      return
    }

    this.saving = true
    this.todos.push({
      name: this.newTodoName,
      isComplete: false
    })

    this.newTodoName = ''
    this.save()
  }

  remove (id: number) {
    this.saving = true
    this.todos = this.todos.filter((_t, i) => {
      return i !== id
    })

    this.save()
  }

  save () {
    this.saving = true
    if (this.todos.length === 0) {
      localStorage.removeItem(Tasks.localStorageKey)
    } else {
      localStorage.setItem(Tasks.localStorageKey, JSON.stringify(this.todos))
    }
    this.saving = false
  }
}
</script>

<style lang="scss" scoped>
.tasks-container {
  margin: 0 auto;
  display: flex;
  justify-content: center;
}

table {
  margin: 1rem;
  font-size: 1.5rem;
  border-collapse: collapse;

  td,
  th {
    padding: 0.5rem;
  }

  tr:not(:first-of-type) {
    td {
      border-top: 1px solid #dee2e6;
    }
  }
}
</style>
