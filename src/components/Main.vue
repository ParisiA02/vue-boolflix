<template>
  <div class="container">
    <h1>BoolFix</h1>
    <input type="text" v-model="title">
    <button @click="search" @keydown.enter="search()">Search</button>
      {{this.apiSearch}}
    <ul>
      <li v-for="film,i in films" :key="i">{{film}}</li>
    </ul>
  </div>
</template>

<script>
import axios from "axios"
export default {
  name: 'Main',
  data(){
    return{
      title:"",
      apiSearch:"",
      films:[],
      apiUrl:"https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&language=it-IT&query="
    }
  },
  methods: {
    search(){
      let apiSearch = this.apiUrl + this.title;
      this.apiSearch = apiSearch;
      axios
      .get(this.apiSearch)
      .then((result)=>{
        let risultato = result.data.results;
        let tempTitle = [];

        for(let i = 0; i < risultato.length ; i++){
          tempTitle.push(risultato[i].title)
        }
        this.films = tempTitle;
      });
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
