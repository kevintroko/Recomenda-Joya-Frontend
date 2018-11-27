<template>
  <div>
    <template>
      <v-list-tile avatar @click="clicked">
        <v-list-tile-content>
          <v-container>
            <v-layout row>{{product.nombre}}</v-layout>
            <v-layout row>
              <v-flex align-content-start>
                <img src="../assets/money.png">
                <span class='text--primary'>$ {{product.precio.toFixed(2)}}</span>
              </v-flex>
              <v-flex align-content-center>
                <img src="../assets/gold_bar.png"> <span class='text--primary'>{{product.kilates}}K</span>
              </v-flex>
              <v-flex align-content-end>
                <img src="../assets/scale.png"> <span class='text--primary'>{{product.peso}}g</span>
              </v-flex>
            </v-layout>
          </v-container>
        </v-list-tile-content>
      </v-list-tile>
      <v-divider inset></v-divider>
    </template>
  </div>
</template>

<script>
export default {
  name: 'SuggestionItem',
  props: ['product'],
  data() {
    return {};
  },
  methods: {
    clicked() {
      console.log(this.product.id);
    }
  }
}
</script>

<style scoped>
</style>
