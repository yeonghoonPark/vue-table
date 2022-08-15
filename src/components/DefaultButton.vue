<template>
  <button @click="btn" :class="isButtonClass">{{ message }}</button>
</template>

<script>
import { computed } from "@vue/reactivity";
export default {
  props: {
    message: {
      type: String,
      default: "default",
    },
    isButton: {
      type: Boolean,
      default: null,
    },
  },
  emits: ["emit-data"],
  setup(props, { emit }) {
    const btn = () => {
      emit("emit-data", "Hello");
    };

    const isButtonClass = computed(() =>
      props.isButton ? "is-save" : "is-close"
    );
    return {
      btn,
      isButtonClass,
    };
  },
};
</script>

<style scoped>
button {
  all: unset;
  width: 100px;
  height: 40px;
  margin: 1rem auto;
  border-radius: 5px;
  border: 2px solid #111101;
  font-weight: 600;
  text-align: center;
  background: #111101;
  color: #ffffff;
  cursor: pointer;
  transition: 0.1s;
}

button:hover {
  /* color: #3dc074; */
  /* color: #111101; */
  /* color: #ffffff; */
  transform: scale(1.1);
}
</style>
