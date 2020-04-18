<template>
  <div class="home" style="margin-top:40px;" id="nav">
    <div class="container">
      <div class="row row-cols-1 row-cols-md-4">
        <div v-for="(pokemon, i) in pokemons" :key="i" class="col mb-4">
          <Pokemon :pokemon="pokemon" :show-open-button="true" />
        </div>
      </div>

      <nav aria-label="Page navigation example">
        <ul class="pagination justify-content-center">
          <li v-if="prev" class="page-item">
            <button v-on:click="prevPage()" class="page-link" href="#" tabindex="-1">Previous</button>
          </li>
          <li class="page-item">
            <button v-on:click="nextPage()" class="page-link">Next</button>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "@/components/Pokemon";

export default {
  name: "Home",

  components: { Pokemon },

  data() {
    return {
      total: null,
      pokemons: [],
      next: "",
      prev: Boolean,
      current: "https://pokeapi.co/api/v2/pokemon/?offset=0&limit=20"
    };
  },

  methods: {
    async getPokemons() {
      await axios
        .get(this.current)
        .then(res => {
          this.pokemons = res.data.results;
          this.next = res.data.next;
          this.prev = res.data.previous;
          this.total = res.data.count;
        })
        .catch(res => {
          console.log(res);
        });
    },
    nextPage() {
      this.current = this.next;
      this.getPokemons();
    },
    prevPage() {
      this.current = this.prev;
      this.getPokemons();
    }
  },
  created() {
    this.getPokemons();
  }
};
</script>

<style>
.list-element {
  margin-bottom: 10px;
  border-bottom: 1px solid #dedede;
}

.float-right {
  float: right;
}

.centered {
  text-align: center;
}
</style>
