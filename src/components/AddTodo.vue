<template>
  <div>
    <b-form inline @submit="addTask">
      <b-form-input placeholder="Add a task" v-model="item"></b-form-input>
      <b-button variant="primary" type="submit">Save</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      item: "",
    };
  },
  methods: {
    addTask(e) {
      e.preventDefault();

      //emit the add-todo event...
      this.$emit("add-todo", {
        id: Math.floor(1000 + Math.random() * 9000),
        item: this.item,
        completed: false,
      });

      //clear the field...
      this.item = "";
    },
  },
};
</script>

<style></style>
