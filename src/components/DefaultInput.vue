<template>
  <input type="text" v-bind="$attrs" v-model="value" />
</template>

<script>
import { computed } from "@vue/reactivity";
export default {
  inheritAttrs: false,
  props: ["modelValue"],
  emits: ["update:modelValue"],
  setup(props, { emit }) {
    const value = computed({
      get() {
        return props.modelValue;
      },
      set(value) {
        emit("update:modelValue", value);
      },
    });
    return { value };
  },
};
</script>

<style lang="scss" scoped></style>
