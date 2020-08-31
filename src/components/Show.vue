<template>
    <div class="show" @click="toggleView">
        <h2>{{ name }}</h2>
        <div v-if="detailView" v-html="summary"></div>
        <img v-else :src="src" />
    </div>
</template>

<script>
export default {
  name: 'Show',
  props: {
     name: String,
     src: String, 
     summary: String,
  },
  data() {
      return {
          detailView: false
      }
  },
  methods: {
      toggleView() {
          this.detailView = !this.detailView
      }
  }
}
</script>

<style scoped>
.show {
  margin: 20px;
  padding: 20px;
  border-radius: 10px;
}
.show:hover {
  background: #f7fafc;
  cursor: pointer;
}

</style>
