<template>
  <div>
    <ul>
      <Item
        v-for="(todo, i) of todos"
        v-bind:todo="todo"
        v-bind:index="i"
        v-bind:key="todo.id"
        v-on:remove-todo="removeItem"
      />
    </ul>
  </div>
</template>

<script>
import Item from "@/components/Item";
export default {
  props: ["todos"],
  components: {
    Item
  },
  methods: {
    removeItem(id) {
      this.$emit("remove-todo", id);
    }
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>