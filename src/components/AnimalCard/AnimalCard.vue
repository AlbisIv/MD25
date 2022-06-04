<template>
  <div></div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "AnimalCard",
  emits: ["addAnimal"],
  data() {
    return {
      inputValue: "",
      typeValue: "cat",
    };
  },
  methods: {
    submitHandler() {
      this.$emit("addAnimal", { name: this.inputValue, type: this.typeValue });

      this.inputValue = "";
    },
  },
});
</script>
