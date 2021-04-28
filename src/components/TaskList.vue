<template>
  <div class="task-list">
    <label class="task-list__title">{{ label }}</label>
    <ul class="task-list__list">
      <li
        class="task-list__list--item"
        v-for="(task, index) in tasklist"
        :key="task.id"
      >
        <span
          class="task-list__list--item__left"
          :class="{ completed: task.completed }"
        >
          <checkbox
            :checked="task.completed"
            :label="task.title"
            @change="updateCheckbox(index)"
          />
        </span>

        <span class="task-list__list--item__right" @click="deleteTask(index)"
          ><img
            class="task-list__list--item__right--image"
            :class="{ completed: task.completed }"
            src="../assets/close.svg"
        /></span>
      </li>
    </ul>
  </div>
</template>

<script>
import Checkbox from "./Checkbox";
export default {
  name: "task-list",
  components: { Checkbox },
  props: {
    tasklist: {
      type: Array,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
  },
  methods: {
    deleteTask(index) {
      this.$emit("deletedTask", index);
    },
    updateCheckbox(index) {
      this.tasklist[index].completed = !this.tasklist[index].completed;
    },
  },
};
</script>
<style lang="scss">
.task-list {
  margin-top: 30px;

  &__title {
    display: flex;
    color: gray;
  }

  &__list {
    list-style-type: none;
    padding: 0;

    &--item {
      left: 0;
      padding: 10px 15px;
      font-size: 20px;
      border: none;
      box-shadow: 3px 5px 5px #ccc;
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      justify-content: space-between;

      &__left {
        display: flex;
        justify-content: space-between;
        &.completed {
          text-decoration: line-through;
          opacity: 30%;
        }
      }

      &__right {
        :hover {
          cursor: pointer;
        }

        &--image {
          height: 15px;
          width: 15px;
          &.completed {
            opacity: 20%;
          }
        }
      }
    }
  }
}
</style>
