<template>
  <div class="container">
    <h2 class="text-center">
      CodeAutomation TodoApp
    </h2>

    <div class="d-flex">
      <input
        type="text"
        class="form-control"
        placeholder="Enter Text"
        v-model="task"
      />

      <button class="btn btn-warning rounded-0" @click="sumitTask">
        SUBMIT
      </button>
    </div>
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">Edit</th>
          <th scope="col" class="text-center">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <th>{{ task.name }}</th>
          <td>{{ task.status }}</td>
          <td>
            <div class="text-center" @click="handleEdit(index)">
              <span class="fa fa-pen"> </span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="handleDelete(index)">
              <span class="fa fa-trash"> </span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      task: "",
      editText: null,
      tasks: [
        { name: "Learn Vue.js", status: "Learning" },
        { name: "Create Simple Todo App", status: "Completed" },
      ],
    };
  },

  methods: {
    sumitTask() {
      console.log("Submit taskss ......", this.task);
      if (this.task.length) {
        if (this.editText === null) {
          this.tasks.push({
            name: this.task,
            status: "to-do",
          });
        } else {
          this.tasks[this.editText].name = this.task;
          this.editText = null;
        }
        this.task = "";
      } else {
        alert("Fileds should not be empty");
      }
    },
    handleDelete(index) {
      this.tasks.splice(index, 1);
    },
    handleEdit(index) {
      this.task = this.tasks[index].name;
      this.editText = index;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
