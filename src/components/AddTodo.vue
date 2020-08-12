<template>
  <div class="addtodo">
    <b-form inline @submit="addTask">
      <b-form-input
        placeholder="Add a task"
        v-model="title"
        class="addtodo_input"
      ></b-form-input>
      <b-button variant="primary" type="submit">Save</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTask(e) {
      e.preventDefault();

      //emit the add-todo event...
      this.$emit("add-todo", {
        id: Math.floor(1000 + Math.random() * 9000),
        title: this.title,
        completed: false,
      });

      //clear the field...
      this.title = "";
    },
  },
};
</script>

<style scoped>
.addtodo {
  display: flex;
}

.addtodo_input {
  margin-right: 0.5rem;
}
</style>
