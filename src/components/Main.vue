<template>
  <div class="container">
    <h1>BoolFix</h1>
    <input type="text" v-model="title">
    <button @click="search" @keydown.enter="search()">Search</button>
    <ul>
      <li>{{this.apiSearch}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Main',
  data(){
    return{
      title:"",
      apiSearch:"",
      apiUrl:"https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&language=it-IT&="
    }
  },
  methods: {
    search(){
      this.title.replace(/\s/g, '+');
      console.log(this.title);
      let apiSearch = this.apiUrl + this.title;
      this.apiSearch = apiSearch;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

ul {
  list-style-type: none;
  padding: 0;
}
</style>
