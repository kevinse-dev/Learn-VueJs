<template>
  <main v-if="!isLoading">
    <DataTitle v-text="title" />
    <div class="w-6/12 bg-red-100 p-10 mx-auto contai">
      <DataBoxes />
      <div v-for="index in pokemon" :key="index" class="">
        <router-link v-bind:to="'/' + index.name">
          <div class="container hover:-translate-y-5 cursor-pointer hover:bg-neutral-50 hover:duration-500 m-5 w-6/12 bg-gray-400 mx-auto shadow-md p-5">
            {{ index.name }}
          </div>
        </router-link>
      </div>
    </div>
  </main>

  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-grey-500 text-3xl mt-10 mb-6">Fetching Data</div>
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes/DataBoxes.vue";

export default {
  name: "Home",
  components: {},
  components: {
    DataTitle,
    DataBoxes,
  },
  data() {
    return {
      isLoading: true,
      title: "Semua Pokemon ada di sini !",
      name: "",
      pokemon: [],
    };
  },
  methods: {
    async fetchAllPokemon() {
      const res = await fetch("https://pokeapi.co/api/v2/pokemon");
      const data = res.json();
      // console.log(data)
      return data;
    },
  },
  async created() {
    const data = await this.fetchAllPokemon();
    (this.name = data.name), (this.pokemon = data.results), (this.isLoading = false);
    console.log(data);
  },
};
</script>
