<template>
  <div class="todo-list">
    <label class="todo-list__title">TO-DO List</label>
    <span class="todo-list__add-task">
      <input
        class="todo-list__add-task--input"
        placeholder="Write your task here"
        v-model="newTask"
      />
      <button class="todo-list__add-task--btn" @click="addTask">
        Add task
      </button>
    </span>
    <task-list
      :tasklist="pendingTasks"
      label="Not finished tasks"
      @deletedTask="deleteTask"
      @updatedTask="updateTask"
    />
    <task-list
      :tasklist="completedTasks"
      label="Finished tasks"
      @deletedTask="deleteTask"
    />
  </div>
</template>

<script>
import TaskList from "./TaskList";
export default {
  name: "todo-list",
  components: { TaskList },
  data() {
    return {
      newTask: "",
      tasks: [
        { id: 1, title: "Read Readme", completed: false },
        { id: 2, title: "Clone this repository", completed: false },
        { id: 3, title: "Install project dependencies", completed: false },
        { id: 4, title: "Run server", completed: false },
      ],
    };
  },
  computed: {
    pendingTasks() {
      return this.tasks.filter((task) => !task.completed);
    },
    completedTasks() {
      return this.tasks.filter((task) => task.completed);
    },
  },

  methods: {
    addTask() {
      if (this.newTask === "") {
        return;
      }
      const newTaskId = this.task
        ? this.tasks[this.tasks.length - 1].id + 1
        : 1;
      this.tasks.push({
        id: newTaskId,
        title: this.newTask,
        completed: false,
      });
      this.newTask = "";
      this.idForTodo++;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    updateTask(value, index) {
      console.log(index);
      this.task[index].completed = value;
    },
  },
};
</script>
<style lang="scss">
.todo-list {
  font-weight: 400;
  display: flex;
  flex-direction: column;

  &__title {
    font-size: 35px;
    margin-bottom: 30px;
  }

  &__add-task {
    display: flex;
    flex-direction: column;
    align-items: center;

    &--input {
      width: 93%;
      padding: 12px 20px;
      font-size: 20px;
      border: none;
      box-shadow: 3px 5px 5px #ccc;
      border-radius: 10px;
      &:focus {
        outline: none;
      }
    }

    &--btn {
      width: 30%;
      border-radius: 25px;
      padding: 10px 15px;
      border: none;
      font-size: 20px;
      background: #2bc016;
      color: white;
      margin-top: 30px;
    }
  }
}
::placeholder {
  color: gray;
}
</style>
