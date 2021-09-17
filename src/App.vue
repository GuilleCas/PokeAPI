<template>
  <div id="PokeAPI">
    <!-- Se define el Background Image -->
    <div
      class="
        min-h-screen
        w-full
        h-full
        bg-no-repeat bg-cover
        items-center
        justify-center
      "
      style="
        background-image: url('https://images.alphacoders.com/100/thumb-1920-1008229.png');
      "
    >
      <!-- Se define el titulo de la pagina -->
      <div>
        <img
          class="mx-auto"
          src="https://cdn2.bulbagarden.net/upload/4/4b/Pok%C3%A9dex_logo.png"
          alt="Pokedex"
        />
      </div>

      <div class="flex flex-row justify-center">
        <div class="my-auto">
          <input
            type="input"
            class="items-center justify-center h-10 w-56"
            v-model="valor"
          />
        </div>
        <div class="px-10">
          <input
            type="button"
            class="
              items-center
              justify-center
              h-11
              w-36
              border border-transparent
              text-base
              font-medium
              rounded-lg
              text-indigo-600
              bg-white
              hover:bg-indigo-50
            "
            value="Buscar"
            v-on:click="buscar"
          />
        </div>
      </div>
      <div class="flex justify-center py-20">
        <div
          v-if="img"
          class="w-56 h-72 rounded border-2 border-gray-900 overflow-hidden"
        >
          <img :src="img" class="w-full h-44" />
          <div class="bg-gray-100 px-6 py-5">
            <div class="font-bold text-center text-xl mb-0">{{ nombre }}</div>
          </div>
          <div class="bg-gray-200 px-4 py-3 pb-0.5">
            <span
              class="
                inline-block
                bg-green-300
                rounded-full
                px-2
                py-1
                text-xs
                font-semibold
                text-gray-700
                mr-1
                mb-1
              "
              >{{ habilidades }}</span
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PokeAPI",

  data() {
    return {
      valor: null,
      pokemon: null,
      nombre: null,
      img: null,
      habilidades: null,
    };
  },

  methods: {
    buscar: function () {
      axios
        .get(`https://pokeapi.co/api/v2/pokemon/${this.valor}`)
        .then((Response) => {
          this.pokemon = Response.data;
          const nombre = Response.data.name;
          this.nombre = nombre;
          //console.log(pokemon);
          const imagen = Response.data.sprites.front_default;
          this.img = imagen;
          const habilidad = Response.data.abilities[0].ability.name;
          this.habilidades = habilidad;
          //console.log(habilidad);
        });
    },
  },
};
</script>

<style>
</style>



