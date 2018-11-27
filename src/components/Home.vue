<template>
  <div>
    <b-container>
      <search-params @change="onParamsChange"></search-params>
      <loading v-if="isLoading"></loading>
      <v-list two-line class="results">
        <suggestion-item
        v-if="!isLoading && loaded"
        v-for="product in results"
        v-bind:key="product.id"
        v-bind:product="product"></suggestion-item>
      </v-list>
    </b-container>
  </div>
</template>

<script>
import SearchParams from './SearchParams'
import SuggestionItem from './SuggestionItem'
import Loading from './Loading'
import API from '../api'

const api = new API();

export default {
  name: 'Home',
  components: { Loading, SuggestionItem, SearchParams },
  props: [ 'userId' ],
  data() {
    return {
      isLoading: false,
      loaded: false,
      query: {
        userId: null,
        minPrice: null,
        maxPrice: null,
        category: null,
      },
      results: [],
    }
  },
  created() {
    if (this.$userId) {
      this.query.userId = this.$userId;
    }
  },
  methods: {
    onParamsChange(query) {
      this.isLoading = true;
      this.query = query;
      api.getSuggestions(this.query)
      .then(this.updateResults)
      .catch(this.$log)
      .finally(() => this.setLoading(false));
    },
    setLoading(loading) {
      this.isLoading = loading;
    },
    updateResults(results) {
      this.loaded = true;
      this.results = results;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.search-bar {
  margin: 10px;
}
.results {
  margin: 30px;
}
</style>
