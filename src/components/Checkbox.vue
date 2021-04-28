<template>
  <label class="checkbox">
    <input
      class="checkbox__input"
      :class="{ checked }"
      type="checkbox"
      :checked="checked"
      @change="handleChange"
    />
    <label class="checkbox__label">{{ label }}</label>
  </label>
</template>

<script>
export default {
  name: "checkbox",
  props: {
    checked: {
      type: Boolean,
      required: false,
    },
    label: {
      type: String,
      required: true,
    },
  },
  methods: {
    handleChange(event) {
      this.$emit("change", event.target.checked);
    },
  },
};
</script>
<style lang="scss">
.checkbox {
  display: inline-flex;
  justify-items: center;
  position: relative;
  align-items: center;
  justify-content: center;
  left: 5px;
  :hover {
    cursor: pointer;
  }

  &__input {
    position: relative;
    appearance: none;
    width: 20px;
    height: 20px;
    border-style: solid;
    border-color: grey;
    border-width: 2px;
    &:before {
      position: absolute;
      background-color: transparent;
      width: 20px;
      height: 20px;
    }

    &.checked {
      &:after {
        position: absolute;
        height: 20px;
        width: 20px;
        left: -1px;

        background-repeat: no-repeat;
        background-position: center;
        content: "";
        background-image: url("../assets/check.svg");
        color: #ccc;
      }
    }
  }
  &__label {
    margin: 0 10px;
    color: black;
  }
}
</style>
