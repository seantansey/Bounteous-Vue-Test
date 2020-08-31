<template>
  <div>
    <input 
      v-model="queryString"
      placeholder="Search terms..."
    >
    <button @click="getTVShowNames">Search for Shows</button>
    <div v-for="(show, index) in shows" :key="index">
      <Show 
        v-if="show.show.image && show.show.image.medium" 
        :name="show.show.name" 
        :src="show.show.image.medium"
        :summary="show.show.summary"
      >
      </Show>
    </div>
  </div>
</template>

<script>
import Show from './Show.vue'

export default {
  name: 'ShowList',
  components:{
    Show,
  },
  data() {
    return {
      queryString: '',
      shows: [],
    }
  },
  methods: {
    async getTVShowNames() {
      try {
        let response = await fetch(`http://api.tvmaze.com/search/shows?q={${this.queryString}}`)
        let json = await response.json()
        json.sort((a,b) => a.show.name > b.show.name ? 1 : ((a.show.name < b.show.name) ? -1 : 0 ))
        this.shows = json
        json.forEach(tvShow => console.log(tvShow.show.name))
      } catch(e) {
        console.log(e)
      }
    },
  },
}
</script>

<style scoped>
input {
  margin: 10px;
}
button {
  margin: 10px;
}
</style>
