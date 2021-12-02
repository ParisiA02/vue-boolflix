<template>
  <div class="container">
    <h1>BoolFix</h1>
    <input type="text" v-model="title" @keydown.enter="search">
    <button @click="search">Search</button>
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
      <li v-if="votes[k] === 0">
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>      
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>
      </li>
      <li v-else-if="votes[k] === 1">
        <i class="fas fa-star"></i>
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>      
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>
      </li>
      <li v-else-if="votes[k] === 2">
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>
        <i class="far fa-star"></i>      
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>
      </li>
      <li v-else-if="votes[k] === 3">
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>      
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>
      </li>
      <li v-else-if="votes[k] === 4">
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>      
        <i class="fas fa-star"></i>
        <i class="far fa-star"></i>
      </li>
      <li v-else-if="votes[k] === 5">
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>      
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>
      </li>

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
      <li v-if="votes[i] === 0">
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>      
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>
      </li>
      <li v-else-if="votes[i] === 1">
        <i class="fas fa-star"></i>
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>      
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>
      </li>
      <li v-else-if="votes[i] === 2">
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>
        <i class="far fa-star"></i>      
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>
      </li>
      <li v-else-if="votes[i] === 3">
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>      
        <i class="far fa-star"></i>
        <i class="far fa-star"></i>
      </li>
      <li v-else-if="votes[i] === 4">
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>      
        <i class="fas fa-star"></i>
        <i class="far fa-star"></i>
      </li>
      <li v-else-if="votes[i] === 5">
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>      
        <i class="fas fa-star"></i>
        <i class="fas fa-star"></i>
      </li>
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
      filmImgUrl:"https://image.tmdb.org/t/p/w300",
      votes: []
    }
  },
  methods: {
    search(){
      let apiFilmSearch="";
      let apiTvSearch="";
      let tempVote=[];

      apiFilmSearch = this.filmApiUrl + this.title;
      apiTvSearch = this.seriesApiUrl + this.title;

      this.apiFilmSearch ="";
      this.apiFilmSearch = apiFilmSearch;
      axios
      .get(this.apiFilmSearch)
      .then((result)=>{
        this.films = result.data.results;
        for(let i=0; i < this.films.length; i++){
          tempVote.push(this.films[i].vote_average);
          this.votes.push(Math.ceil(tempVote[i]/2));
        }
      });

      this.apiTvSearch ="";   
      this.apiTvSearch = apiTvSearch;
      axios
      .get(this.apiTvSearch)
      .then((result)=>{
        this.tvSeries = result.data.results;
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
