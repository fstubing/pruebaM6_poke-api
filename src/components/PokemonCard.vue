<template>
  <div class="col">
    <div class="card h-100 d-flex flex-column align-items-center">
      <img :src="image" :style="filtroGris" class="card-img-top" />
      <input
        v-if="!descubierto"
        v-model="userInput"
        @keyup.enter="checkName"
        class="form-control w-50 mt-3"
      />
      <button
        v-if="!descubierto"
        @click="checkName"
        class="btn btn-secondary w-50 my-3"
      >
        Descubrir
      </button>
      <div v-if="descubierto" class="text-center my-3">{{ name }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonCard",
  props: ["name", "image"],
  data() {
    return {
      userInput: "",
      descubierto: false,
    };
  },
  computed: {
    filtroGris() {
      return this.descubierto ? "" : "filter: blur(5px) grayscale(100%);";
    },
  },
  methods: {
    checkName() {
      if (this.userInput.toLowerCase() === this.name.toLowerCase()) {
        this.descubierto = true;
        this.$emit("nameChecked", true);
      } else {
        alert("Nombre incorrecto");
        this.$emit("nameChecked", false);
      }
    },
  },
};
</script>

<style scoped></style>
