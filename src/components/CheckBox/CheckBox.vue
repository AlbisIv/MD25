<template>
  <div>
    <form @submit.prevent="submitHandler">
      <input type="text" v-model="inputValue" />
      <select v-model="typeValue" name="type" id="type">
        <option value="cat">Cat</option>
        <option value="dog">Dog</option>
      </select>
      <button type="submit">Add animal</button>
    </form>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "AnimalAdder",
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
