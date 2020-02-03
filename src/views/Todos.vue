<template>
  <div>
    <h2>Todo list page</h2>
    <router-link to="/">Home</router-link>
    <hr />
    <div class="nav-bar">
      <AddItem @add-todo="AddItem" />
      <select v-model="filter" v-if="!isLoading">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not Completed</option>
      </select>
    </div>
    <hr />
    <Spinner v-if="isLoading" />
    <List v-else-if="filtered.length" v-bind:todos="filtered" @remove-todo="removeItem" />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import List from "@/components/List";
import AddItem from "@/components/AddItem";
import Spinner from "@/components/Spinner";
export default {
  name: "app",
  data() {
    return {
      todos: [],
      isLoading: true,
      filter: "all"
    };
  },
  components: {
    List,
    AddItem,
    Spinner
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=7")
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json;
          this.isLoading = false;
        }, 300);
      });
  },
  computed: {
    filtered() {
      switch (this.filter) {
        case "all": {
          return this.todos;
        }
        case "completed": {
          return this.todos.filter(t => t.completed);
        }
        case "not-completed": {
          return this.todos.filter(t => !t.completed);
        }
        default: {
          return this.todos;
        }
      }
    }
  },
  methods: {
    removeItem(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    },
    AddItem(todo) {
      this.todos.push(todo);
    }
  }
};
</script>

<style scoped>
.nav-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}
</style>