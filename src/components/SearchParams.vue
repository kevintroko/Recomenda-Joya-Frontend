<template>
  <div>
    <v-layout row>
      <v-flex shrink class="price-field">
        <v-text-field
          v-model="price[0]"
          class="mt-0"
          hide-details
          single-line
          type="number"
        ></v-text-field>
      </v-flex>

      <v-flex class="px-3">
        <v-range-slider
          v-model="price"
          @change="onChange"
          :max="maxPrice"
          :min="minPrice"
        ></v-range-slider>
      </v-flex>

      <v-flex shrink class="price-field">
        <v-text-field
          v-model="price[1]"
          class="mt-0"
          hide-details
          single-line
          type="number"
        ></v-text-field>
      </v-flex>
    </v-layout>

    <v-btn-toggle max=5 mandatory v-model="category" @change="onChange">
      <v-btn 
        flat
        v-for="category in categories"
        v-bind:key="category"
        :value="category">
        <span>{{category}}</span>
      </v-btn>
    </v-btn-toggle>
  </div>
</template>
<script>

const maxPrice = 60000;
const minPrice = 0;

const categories = [
  "anillo",
  "argolla",
  "arete",
  "juegos",
  "broquel",
  "arracada",
  "huggie",
  "medalla",
  "cristo",
  "dije",
  "cadena",
  "esclava",
  "aro",
  "semanario",
  "reloj",
  "gargantilla",
  "rosario",
]

export default {
  name: 'SearchParams',
  data(){
    return {
      maxPrice,
      minPrice,
      categories,

      category: categories[0],
      price: [minPrice, maxPrice],
    };
  },
  created() {
    this.onChange();
  },
  methods: {
    onChange() {
      this.$emit('change', {
        category: this.category,
        minPrice: this.price[0],
        maxPrice: this.price[1],
      });
    },
  },
}
</script>

<style scoped>
.price-field {
  width: 40px
}
</style>
