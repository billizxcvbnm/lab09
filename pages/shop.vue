<template>
  <div>
    <v-text-field v-model="query" label="Search"></v-text-field>
    <v-btn @click="handleSearchShop">Search</v-btn>

    <v-divider class="mt-2 mb-2"></v-divider>
    <div class="d-flex flex-wrap">
      <v-card
        v-for="shop in results"
        :key="shop.mal_id"
        class="ma-2"
        max-width="344"
        outlined
        @click="handleShopClick(shop)"
      >
        <v-list-item three-line>
          <v-list-item-content>
            <div class="overline mb-4">Publishing: {{ shop.publishing }}</div>
            <v-list-item-title class="headline mb-1">
              {{ shop.title }}
            </v-list-item-title>
            <v-list-item-subtitle>
              {{ shop.synopsis }}
            </v-list-item-subtitle>
          </v-list-item-content>

          <img
            :src="shop.image_url"
            alt=""
            :style="{ width: '80px', marginTop: '10px' }"
          />
        </v-list-item>
      </v-card>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      query: '',
      results: [],
    }
  },
  methods: {
    handleSearchShop() {
      const url = `https://api.jikan.moe/v3/search/manga?q=${this.query}&page=1`
      axios.get(url).then((res) => {
        console.log(res)
        this.results = res.data.results
      })
    },
    handleShopClick(shop) {
      console.log('SHOP', shop)
      window.location = shop.url
    },
  },
}
</script>

<style></style>
