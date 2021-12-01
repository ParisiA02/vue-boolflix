<template>
  <div class="container">
    <h1>BoolFix</h1>
    <input type="text" v-model="title">
    <button @click="search" @keydown.enter="search()">Search</button>
    <ul v-for="film,k in films" :key="'A' + k">
      <li>{{film.title}}</li>
      <li>{{film.original_title}}</li>
      <li v-if="film.backdrop_path !== null"> <img :src="filmImgUrl + film.backdrop_path" alt="img"></li>
      <li v-else>IMMAGINE ASSENTE</li>
      <li v-if="film.original_language === 'en'"> <img src="../assets/inghilterra.png" alt="en-flag"> </li>
      <li v-else-if="film.original_language === 'it'"> <img src="../assets/italia.png" alt="ita-flag"> </li>
      <li v-else-if="film.original_language === 'es'"> <img src="../assets/spagna.png" alt="es-flag"> </li>
      <li v-else-if="film.original_language === 'fr'"> <img src="../assets/francia.png" alt="fr-flag"> </li>
      <li v-else>{{film.original_language}}</li>
      <li>{{'voto'}}</li>
    </ul>
    <ul v-for="serie,i in tvSeries" :key="'B' + i">
      <li>{{serie.name}}</li>
      <li>{{serie.original_name}}</li>
      <li v-if="serie.backdrop_path !== null"> <img :src="filmImgUrl + serie.backdrop_path" alt="img"></li>
      <li v-else>IMMAGINE ASSENTE</li>
      <li v-if="serie.original_language === 'en'"> <img src="../assets/inghilterra.png" alt="en-flag"> </li>
      <li v-else-if="serie.original_language === 'it'"> <img src="../assets/italia.png" alt="ita-flag"> </li>
      <li v-else-if="serie.original_language === 'es'"> <img src="../assets/spagna.png" alt="es-flag"> </li>
      <li v-else-if="serie.original_language === 'fr'"> <img src="../assets/francia.png" alt="fr-flag"> </li>
      <li v-else>{{serie.original_language}}</li>
      <li>{{'voto'}}</li>
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
      apiFilmSearch:"",
      apiTvSearch:"",
      filmApiUrl:"https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&language=it-IT&query=",
      seriesApiUrl:"https://api.themoviedb.org/3/search/tv?api_key=e99307154c6dfb0b4750f6603256716d&language=it_IT&query=",
      films:[],
      tvSeries:[],
      filmImgUrl:"https://image.tmdb.org/t/p/w185"
    }
  },
  methods: {
    search(){
      let apiFilmSearch="";
      let apiTvSearch="";

      apiFilmSearch = this.filmApiUrl + this.title;
      apiTvSearch = this.seriesApiUrl + this.title;

      this.apiFilmSearch ="";
      this.apiFilmSearch = apiFilmSearch;
      axios
      .get(this.apiFilmSearch)
      .then((result)=>{
        this.films = result.data.results;
      });

      this.apiTvSearch ="";   
      this.apiTvSearch = apiTvSearch;
      axios
      .get(this.apiTvSearch)
      .then((result)=>{
        this.tvSeries = result.data.results;
      });
      
    console.log(this.apiTvSearch);
    console.log(this.apiFilmSearch);
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
