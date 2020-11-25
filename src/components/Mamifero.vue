<template>
  <div>
    <h4 v-if="mammal_animal">El animal es: {{ mammal_animal }}</h4>
    <div v-if="mammal_type.whale == 2">
      <small> El otro tipo era un Tigre </small>
      <br /><br />
    </div>
    <button :disabled="animal_type_selected.includes(0)" @click="whale(0)">
      Come plancton
    </button>
    <button :disabled="animal_type_selected.includes(2)" @click="tiger(2)">
      Come carne
    </button>
    <button :disabled="animal_type_selected.includes(1)" @click="whale(1)">
      Vive en el mar
    </button>
    <p><button @click="reset()">reset</button></p>
  </div>
</template>

<script>
export default {
  name: "Mamifero",
  data() {
    return {
      mammal_type: { tiger: 0, whale: 0 },
      animal_type_selected: [],
    };
  },
  methods: {
    tiger(n) {
      this.mammal_type.tiger++;
      this.animal_type_selected.push(n);
    },
    whale(n) {
      this.mammal_type.whale++;
      this.animal_type_selected.push(n);
    },
    reset() {
      this.mammal_type.tiger = 0;
      this.mammal_type.whale = 0;
      this.animal_type_selected = [];
    },
  },
  computed: {
    mammal_animal() {
      if (this.mammal_type.tiger == this.mammal_type.whale) {
        return "";
      }
      if (this.mammal_type.tiger > this.mammal_type.whale) {
        return "Tigre";
      }
      if (this.mammal_type.tiger < this.mammal_type.whale) {
        return "Ballena";
      }
      return "";
    },
  },
};
</script>

<style>
</style>