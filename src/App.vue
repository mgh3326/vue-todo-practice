<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>

<script>
  import TodoHeader from "@/components/TodoHeader";
  import TodoInput from "@/components/TodoInput";
  import TodoFooter from "@/components/TodoFooter";
  import TodoList from "@/components/TodoList";

  export default {
    name: 'app',
    data() {
      return {
        todoItems: []
      }
    },
    methods: {
      // TODO 메소드를 store.js로 옮기기(vuex)
      removeOneItem(todoItem, index) {
        localStorage.removeItem(todoItem.item);
        this.todoItems.splice(index, 1);
      },
      toggleOneItem(todoItem, index) {
        this.todoItems[index].completed = !this.todoItems[index].completed;
        localStorage.removeItem(todoItem.item);
        localStorage.setItem(todoItem.item, JSON.stringify(todoItem))
      },
      clearAllItems() {
        localStorage.clear();
        this.todoItems = []
      }
    },

    components: {
      TodoHeader,
      TodoFooter,
      TodoList,
      TodoInput,
    }
  }
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F6;
  }

  input {
    border-style: groove;
    width: 200px;
  }

  button {
    border-style: groove;
  }

  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
