<template>
  <div class="card">
    <div class="card-header"><h4 class="my-0 font-weight-normal">{{ pokemon.name }}</h4></div>
    <div class="card-body">
      <div class="d-flex justify-content-between align-items-center">
        <router-link v-if="showOpenButton" :to="`/pokemons/${pokemon.id}`">
          <button type="button" class="btn btn-secondary">View</button>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "Pokemon",

  props: {
    pokemon: Object,
    /* data() {
      return {
        name: '',
        id: null,
        images: [],
        abilities: [],
        moves: []
      }
    }, */
    showOpenButton: {
      type: Boolean,
      default: false
    },

  }
}
</script>
