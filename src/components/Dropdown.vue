<template>
  <div>
    <button @click="isOpen = true">
      {{ placeholder || modelValue?.label }}
    </button>
    <ul v-if="isOpen">
      <li v-for="item in options" :key="item.value" @click="clickItem(item)">
        {{ item.label }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import type { PropType } from "vue";

export type Option = {
  label: string;
  value: string;
};

export default defineComponent({
  props: {
    placeholder: {
      type: String,
      default: "",
    },
    options: {
      type: Array as PropType<Option[]>,
      required: true,
    },
    modelValue: {
      type: Object as PropType<Option>,
      default: undefined,
    },
  },
  emits: ["update:modelValue"],
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    clickItem(item: Option) {
      this.$emit("update:modelValue", item);
      this.isOpen = false;
    },
  },
});
</script>
