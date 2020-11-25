<template>
  <div>
    <h4 v-if="ave_animal">El animal es: {{ ave_animal }}</h4>
    <div v-if="animal_type.flam == 2">
      <small> El otro tipo era un Albatros </small>
      <br /><br />
    </div>
    <div>
      <button :disabled="animal_type_selected.includes(1)" @click="flam(1)">
        Tiene patas largas
      </button>
      <button :disabled="animal_type_selected.includes(2)" @click="alb(2)">
        Come peces
      </button>
      <button :disabled="animal_type_selected.includes(0)" @click="flam(0)">
        Vive en marisma
      </button>

      <p><button @click="reset()">reset</button></p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Ave",
  data() {
    return {
      animal_type: { flam: 0, alb: 0 },
      animal_type_selected: [],
    };
  },
  methods: {
    flam(n) {
      this.animal_type.flam++;
      this.animal_type_selected.push(n);
    },
    alb(n) {
      this.animal_type.alb++;
      this.animal_type_selected.push(n);
    },
    reset() {
      this.animal_type.flam = 0;
      this.animal_type.alb = 0;
      this.animal_type_selected = [];
    },
  },
  computed: {
    ave_animal() {
      if (this.animal_type.flam == this.animal_type.alb) {
        return "";
      }
      if (this.animal_type.flam > this.animal_type.alb) {
        return "Flamenco";
      }
      if (this.animal_type.flam < this.animal_type.alb) {
        return "Albatros";
      }
      return "";
    },
  },
};
</script>

<style>
</style>
