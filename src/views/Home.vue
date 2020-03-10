<template>
  <div class="home" style="margin-top:40px;">
    <div class="container">
    <div class="row row-cols-1 row-cols-md-4">
      <div v-for="(pokemon, i) in pokemons" :key="i" class="col mb-4">
        <div class="card">
          <img src="" class="card-img-top" alt="">
          <div class="card-header">
            <h4 class="my-0 font-weight-normal">{{ pokemon.name }}</h4>
          </div>
          <div class="card-body">
            <div class="d-flex justify-content-between align-items-center">
                <div class="btn-group">
                  <button type="button" class="btn btn-sm btn-outline-secondary">View</button>
                  <button type="button" class="btn btn-sm btn-outline-secondary">Edit</button>
                </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <nav aria-label="Page navigation example">
      <ul class="pagination justify-content-center">
        <li v-if="prev" class="page-item">
          <a class="page-link" href="#" tabindex="-1">Previous</a>
        </li>
        <li class="page-item">
          <a class="page-link" href="#">Next</a>
        </li>
      </ul>
      <p class="text-center">Mostrando {{this.next.substr(-2)}} de {{this.total}}</p>
    </nav>


    <!--<ul>
      <li v-for="(pokemon, i) in pokemons" :key="i">
        {{ pokemon.name }}
      </li>
    </ul>-->
  </div></div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",

  data() {
    return {
      total: null,
      pokemons: [],
      next: '',
      prev: Boolean
    };
  },

  async created() {
    const res = await axios.get("https://pokeapi.co/api/v2/pokemon/");
    this.pokemons = res.data.results;
    this.next = res.data.next;
    this.prev = res.data.previous;
    this.total = res.data.count;
    //console.log(this.pokemons)
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
