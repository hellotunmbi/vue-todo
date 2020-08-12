<template>
  <div class="todoitem">
    <span class="small" @click="$emit('del-todo', todo.id)"
      >[ <a>close</a> ]</span
    >
    <b-form-checkbox
      :name="todo.item"
      :class="{ completed: todo.completed }"
      v-model="todo.completed"
      @change="markCompleted"
    >
      {{ todo.title }}
    </b-form-checkbox>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markCompleted() {
      this.todo.completed = !this.todo.completed;
    },
  },
};
</script>

<style scoped>
.todoitem {
  display: flex;
  flex-direction: row;
}

.completed {
  text-decoration: line-through;
}

.small {
  font-size: 10px;
  color: red;
  cursor: pointer;
}
</style>
