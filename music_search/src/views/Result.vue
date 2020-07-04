<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
      <v-flex>
        <h1 class="display-1 font-weight-bold mb-3">
          検索結果
        </h1>
        <p>検索キーワード: {{ $route.params.keyword }}</p>
      </v-flex>

      <v-flex 
        mb-5 
        xs12
      >
        <div style="margin-bottom:10px" v-for="(album, i) in albums"
            :key="i"
        >
          <v-card
              color="black"
              dark
              :href="album.collectionViewUrl"
              target="_blank"
              
          >
              <div class="d-flex flex-no-wrap justify-space-between">
                <div>
                  <v-card-title
                    class="headline"
                    v-text="album.collectionName"
                  ></v-card-title>

                  <v-card-subtitle v-text="album.artistName"></v-card-subtitle>
                </div>

                <v-avatar
                  class="ma-3"
                  size="125"
                  tile
                >
                  <v-img :src="album.artworkUrl100"></v-img>
                </v-avatar>
              </div>
          </v-card>
        </div>
      </v-flex>
    </v-layout>
  </v-container>
</template>
<script>
import axios from 'axios'

export default {
  data(){
    return {
      albums: [],
    }
  },
  created(){
    const vm =this
    axios.get(`https://itunes.apple.com/search?term=${this.$route.params.keyword}&entity=album`)
      .then(response => {
        console.log(response)
        vm.albums = response.data.results

      })
  }
}
</script>