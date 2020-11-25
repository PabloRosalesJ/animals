<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />

    <h3>Tipo de animal: {{ animal }}</h3>
    <div v-if="!view.animal">
      <small v-if="animal_type.bird === 3">El otro tipo es Mamifero</small>
      <br />
      <br />
      <button :disabled="animal_type_selected.includes(0)" @click="bird(0)">
        Pone huevos
      </button>
      <button :disabled="animal_type_selected.includes(4)" @click="mammal(4)">
        Da leche
      </button>
      <button :disabled="animal_type_selected.includes(1)" @click="bird(1)">
        Tiene plumas
      </button>
      <button :disabled="animal_type_selected.includes(3)" @click="mammal(3)">
        Tiene Piel
      </button>
      <button :disabled="animal_type_selected.includes(2)" @click="bird(2)">
        Vuela
      </button>
      <p>
        <button @click="reset()">Reset</button>
        <button v-if="animal != ''" @click="next()">Next</button>
      </p>
    </div>
    <div v-if="view.animal_type">
      <div v-if="animal === 'Ave'">
        <Ave></Ave>
      </div>
      <div v-if="animal === 'Mamifero'">
        <Mamifero></Mamifero>
      </div>
    </div>
    <br />
    <a href="/animals/">
      <button>/</button>
    </a>
  </div>
</template>

<script>
import Ave from "./components/Ave";
import Mamifero from "./components/Mamifero";

export default {
  name: "App",
  components: {
    Ave,
    Mamifero,
  },
  data() {
    return {
      view: { animal: false, animal_type: false },
      buttons: { netx_type: true },
      animals: { bird: ["Flamenco", "Albatros"], mammal: ["Tigre", "Ballena"] },
      animal_type_name: "",
      animal_type: { bird: 0, mammal: 0 },
      animal_type_selected: [],
      // bird_type: { albatross: 0, flamengo: 0 },
      // mammal_type: { tiger: 0, whale: 0 },
    };
  },
  methods: {
    bird(n) {
      this.animal_type.bird++;
      this.animal_type_selected.push(n);
    },
    mammal(n) {
      this.animal_type.mammal++;
      this.animal_type_selected.push(n);
    },
    reset() {
      this.animal_type.bird = 0;
      this.animal_type.mammal = 0;
      this.animal_type_selected = [];
      this.type = "";
    },
    next() {
      this.view.animal = true;
      this.view.animal_type = true;
      this.animal_type_name = this.animal;
    },
  },
  computed: {
    animal() {
      if (this.animal_type.bird == this.animal_type.mammal) {
        return "";
      }
      if (this.animal_type.bird > this.animal_type.mammal) {
        return "Ave";
      }
      if (this.animal_type.bird < this.animal_type.mammal) {
        return "Mamifero";
      }
      return "";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
