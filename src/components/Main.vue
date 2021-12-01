<template>
  <div class="container">
    <h1>BoolFix</h1>
    <input type="text" v-model="title">
    <button @click="search" @keydown.enter="search()">Search</button>
      {{this.apiSearch}}
    <ul v-for="film,k in films" :key="k">
      <li v-for="title,i in film.titles" :key="i">{{title}}</li>
      <li v-for="originalTitle,i in film.originalTitles" :key="'A'+ i">{{originalTitle}}</li>
      <li v-for="language,i in film.languages" :key="'B'+ i">{{language}}</li>
      <li v-for="vote,i in film.votes" :key="'C'+ i">{{vote}}</li>
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
      apiUrl:"https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&language=it-IT&query=",
      films:[
        {
          titles:[],
          originalTitles:[],
          languages:[],
          votes:[]
        }
      ]
    }
  },
  methods: {
    search(){
      let apiSearch="";
      apiSearch = this.apiUrl + this.title;
      this.apiSearch = apiSearch;
      axios
      .get(this.apiSearch)
      .then((result)=>{
        let risultato = result.data.results;
        for(let i = 0; i < risultato.length ; i++){
          
            this.films.push(
              this.films[i].titles.push(risultato[i].title),
              this.films[i].originalTitles.push(risultato[i].original_title),
              this.films[i].languages.push(risultato[i].original_language),
              this.films[i].votes.push(risultato[i].vote_average)
            )
            console.log(this.films);
          
        }
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
