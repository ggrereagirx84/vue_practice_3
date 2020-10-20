<template>
  <div>
    <h1>ToDoリスト</h1>
    <fieldset>
      <label>
        <input 
          type="radio" 
          value="すべて" 
          v-model="todoStatus"
          @click="todoDisplay"
        >すべて
      </label>
      <label>
        <input 
          type="radio" 
          value="作業中" 
          v-model="todoStatus"
          @click="todoDisplay"
        >作業中
      </label>
      <label>
        <input 
          type="radio" 
          value="完了" 
          v-model="todoStatus"
          @click="todoDisplay"
        >完了
      </label>
    </fieldset>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>コメント</th>
          <th>状態</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in todos" :key="todo.index" :class="{hidden: todoDisplay(index)}">
          <td>{{ index }}</td>
          <td>{{ todo.content }}</td>
          <td><button @click="toggleStatus(index)">{{ todo.status }}</button></td>
          <td><button @click.prevent="deleteItem(index)">削除</button></td>
        </tr>
      </tbody>
    </table>
    <h2>新規タスクの追加</h2>
    <form>
      <input type="text" v-model="newItem">
      <input type="submit" value="追加" @click.prevent="addItem">
    </form>
  </div>
</template>

<script>


export default {
  data() {
    return {
      todos: [],
      todoStatus: 'すべて',
      newItem: '',
    }
  },
  methods: {
    addItem() {
      this.todos.push({content: this.newItem, status: '作業中'});
      this.newItem = '';
    },
    deleteItem(index) {
      this.todos.splice(index, 1);
    },
    todoDisplay(index) {
      if (this.todoStatus === 'すべて') {
        return false;
      } else if (this.todoStatus === '作業中') {
        if (this.todos[index].status === '作業中') {
          return false;
        } else {
          return true;
        }
      } else if (this.todoStatus === '完了') {
        if (this.todos[index].status === '完了') {
          return false;
        } else {
          return true;
        }
      }
    },
    toggleStatus(index) {
      if (this.todos[index].status === '作業中') {
        this.todos[index].status = '完了';
      } else {
        this.todos[index].status = '作業中';
      }
    }
  }
}
</script>

<style>
  fieldset {
    border: none;
  }
  .hidden {
    display: none;
  }
</style>
