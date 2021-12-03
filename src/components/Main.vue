<template>
  <div class="container">
  <header>
    <h1>BoolFix</h1>
    <div class="search-container">
      <input type="text" v-model="title" @keydown.enter="search">
      <button @click="search">Search</button>
    </div>
  </header>
    <div class="card-container">
        <div class="card" v-for="film,k in films" :key="'A' + k">
          <div class="img-container" v-if="film.poster_path !== null"> <img :src="filmImgUrl + film.poster_path" alt="img"></div>
          <div v-else> <img class="default-img" src="../assets/film.png" alt="default-film-img"></div>
          <ul>
            <li>Titolo: {{film.title}}</li>
            <li>Titolo Originale: {{film.original_title}}</li> 
            <li v-if="film.original_language === 'en'"> Lingua: <img class="img-lingua" src="../assets/inghilterra.png" alt="en-flag"> </li>
            <li v-else-if="film.original_language === 'it'"> Lingua: <img class="img-lingua" src="../assets/italia.png" alt="ita-flag"> </li>
            <li v-else-if="film.original_language === 'es'"> Lingua: <img class="img-lingua" src="../assets/spagna.png" alt="es-flag"> </li>
            <li v-else-if="film.original_language === 'fr'"> Lingua: <img class="img-lingua" src="../assets/francia.png" alt="fr-flag"> </li>
            <li v-else>Lingua: {{film.original_language}}</li>
            <ul class="star-container">
              <li v-for="vote,j in votes" :key="'J'+j">
                <span v-if="j < 5">
                  <span v-if="j < votes[k]"><i class="fas fa-star"></i></span>
                  <span v-else><i class="far fa-star"></i></span>
                </span>
              </li>
            </ul>
            <li>Overview: {{overviews[k]}}</li>
          </ul>
        </div>
        <div class="card" v-for="serie,i in tvSeries" :key="'B' + i">
          <div class="img-container" v-if="serie.poster_path !== null"> <img :src="filmImgUrl + serie.poster_path" alt="img"></div>
          <div v-else> <img class="default-img" src="../assets/tvserie.png" alt="default-serie-img"></div>
          <ul>
            <li>Titolo: {{serie.name}}</li>
            <li>Titolo Originale: {{serie.original_name}}</li>
            <li v-if="serie.original_language === 'en'"> Lingua: <img class="img-lingua" src="../assets/inghilterra.png" alt="en-flag"> </li>
            <li v-else-if="serie.original_language === 'it'"> Lingua: <img class="img-lingua" src="../assets/italia.png" alt="ita-flag"> </li>
            <li v-else-if="serie.original_language === 'es'"> Lingua: <img class="img-lingua" src="../assets/spagna.png" alt="es-flag"> </li>
            <li v-else-if="serie.original_language === 'fr'"> Lingua: <img class="img-lingua" src="../assets/francia.png" alt="fr-flag"> </li>
            <li v-else>Lingua: {{serie.original_language}}</li>
            <ul class="star-container">
              <li v-for="vote,j in votes" :key="'J'+j">
                <span v-if="j < 5">
                  <span v-if="j < votes[i]"><i class="fas fa-star"></i></span>
                  <span v-else><i class="far fa-star"></i></span>
                </span>
              </li>
            </ul>
            <li>Overview: {{overviews[i]}}</li>
          </ul>
        </div>
    </div>
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
      filmImgUrl:"https://image.tmdb.org/t/p/w342",
      votes: [],
      overviews: []
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
        this.votes = [];
        this.overviews = [];
        for(let i=0; i < this.films.length; i++){
          tempVote.push(this.films[i].vote_average);
          this.votes.push(Math.ceil(tempVote[i]/2));
          this.overviews.push(this.films[i].overview);
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

@import '~@fortawesome/fontawesome-free/css/all.min.css';

header{
  width: 100%;
  height: 75px;
  background-color: black;
  display: flex;
  align-items: center;
  justify-content: space-between;

  h1{
    margin-left: 50px;
    color: red;
  }

  .search-container{
    margin-right: 50px;

    input{
      height: 30px;
      margin-right: 10px;
    }

    button{
      padding: 5px;
    }
  }
}

.container{

  width: 100%;
  min-height: 100vh;
  background-color: rgb(54, 50, 50);

  ul {
    list-style-type: none;
    padding: 0;
  }
  .card-container{
    width: 100%;
    display:  flex;
    flex-wrap: wrap;
    margin: 0 auto;
  
    .default-img{
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  
    .card{
      width: calc(100%/5 - 40px);
      height: 500px;
      position: relative;
      border: 1px solid white;
      margin: 20px;
      overflow: auto;
  
      &:hover{
        background-color: black;
        img{
          display: none;
        }

        img.img-lingua{
          display: inline-block;
          width: 20px;
        }

        ul li{
          display: block;
          margin: 10px 0 0 10px;

        }
          ul{
            margin-top: 10px;
          }
          ul.star-container li{
            display: inline;
            color: gold;
          }
      }
  
      img{
        position: absolute;
        width: 100%;
        height: 100%;
      }

      ul li{
        position: relative;
        z-index: 2;
        color: white;
        display: none;
      }
    }
  }
}
</style>
