<!-- TODO   -->
<template>
  <div class="container">
    <AnimalAdder @addAnimal="addAnimal" />
    <br /><br />
    {{ viewMode === "all" ? "Show only C" : "Show All" }}
    <input @click="toggleView" />

    <br /><br />
    <div
      v-for="(animal, index) in animalsView"
      :key="animal.name"
      class="animal"
    >
      <h1>
        {{ animal }}
      </h1>
      <button @click="removeAnimal(index)">Delete</button>
    </div>
    <h1 v-if="loading">Loading.....</h1>
    <div v-for="{ id, name } in characters" :key="id">{{ name }}</div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AnimalAdder from "@/components/AnimalAdder/AnimalAdder.vue";

type ViewMode = "all" | "only-c";
type Animal = {
  name: string;
  type: string;
};

export default defineComponent({
  name: "HomeView",
  components: {
    AnimalAdder,
  },
  data: () => ({
    animalType: "",
    count: 10,
    viewMode: "all" as ViewMode,
    animals: [] as Animal[],
    loading: false,
    characters: [],
  }),
  created() {
    this.animals = JSON.parse(localStorage.getItem("animals") || "[]");
  },
  computed: {
    animalsView() {
      if (this.viewMode === "only-c") {
        return this.animalsStartingWithC;
      }

      return this.animals;
    },
    animalsStartingWithC() {
      return this.animals.filter(({ name }) => name[0].toUpperCase() === "C");
    },
  },
  methods: {
    toggleView() {
      if (this.viewMode === "all") {
        this.viewMode = "only-c";
      } else {
        this.viewMode = "all";
      }
    },
    addAnimal(animal: Animal) {
      const newAnimals = [...this.animals];

      newAnimals.push(animal);

      this.animals = newAnimals;
    },
    removeAnimal(index: number) {
      const newAnimals = [...this.animals];

      newAnimals.splice(index, 1);

      this.animals = newAnimals;
    },
  },
  watch: {
    animals(newAnimals, oldAnimals) {
      localStorage.setItem("animals", JSON.stringify(newAnimals));
    },
  },
});
</script>
<style scoped lang="scss">
.animal {
  display: flex;
  align-items: center;
  gap: 10px;
  justify-content: center;

  h1 {
    margin: 0;
  }
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    justify-content: center;
  }
}
</style>
