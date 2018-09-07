<template>
  <body>
    <div class="movie-list-container">
      <!-- <img src="../assets/film.svg" class="movie-list-container__icon"> -->
      <!-- <p>Your movie is : {{info}}</p> -->
      <div class="movie-list-container__user">Hello, {{email}}!</div>
      <form id="lead-form" @submit.prevent="processForm" v-on:submit: @submit>
              <h1>Find a movie</h1>
              <div>
                <div>
                  <input type="text" class="form-control search-input" placeholder="Enter a movie title" v-model="findMovie">
                  <div class="submit-button">
                    <button id="submit-form">Go!</button>
                  </div>
                  <div class="movie-info">
                    <span class="movie-info__title">{{movieInfoResults.Title}} </span>
                    <span class="movie-info__year">{{movieInfoResults.Year}}</span>
                    <span class="movie-info__genre">{{movieInfoResults.Genre}}</span>
                    <span class="movie-info__rating">{{movieInfoResults.imdbRating}}</span>
                    <span class="movie-info__plot">{{movieInfoResults.Plot}}</span>
                    <span class="movie-info__production">{{movieInfoResults.Production}}</span>
                  </div>
                </div>
              </div>
              <!-- <div>
                <div>
                  <button id="submit-form">Submit</button>
                </div>
              </div> -->
              <button v-if="showAddToMovieListButton" @click="addToMovieList" id="addMovieToList" class="hvr-forward">Add to Movie List</button>
      </form>
      <towatch-list :movieListTitle="movieListTitle"></towatch-list>
    </div>
  </body>
</template>
<script src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="crossorigin="anonymous"></script>
<script type="text/javascript">
import TowatchList from './TowatchList';
import axios from 'axios';
import firebase from 'firebase';
import $ from 'jquery';

// import { bus } from '../main';

export default {
      components: {
        TowatchList
      },
      name: 'movie-list',
      data () {
        return {
          // info: '',
          findMovie: '',
          movieInfoResults: '',
          userId: '',
          name: '',
          email: '',
          user: {},
          movieListTitle: ''
        }
      },
      watch: {
       findMovie: function() {
         this.movieInfoResults = ''
         if (this.findMovie.length >= 0) {
           this.lookupfindMovie()
         }
       },
     },
     created() {
        this.user = firebase.auth().currentUser;
        if(this.user) {
          this.name = this.user.displayName;
          this.email = this.user.email;
          this.photo = this.user.photoURL;
          this.userId = this.user.uid;
        }
      },
       computed: {
         showAddToMovieListButton(){
           if (this.findMovie.length > 0){
             return this.movieInfoResults;
           }
         }
       },
       methods: {
        lookupfindMovie: function() {
          app.movieInfoResults = "Searching..."
        },
        processForm: function() {
          var app = this
          axios.get('http://www.omdbapi.com/?t=' + app.findMovie + '&r=json&tomatoes=true' + '&apikey=991cf08e')
                .then(function (response) {
                  // app.movieInfoResults = response.data.Title + ' , ' + response.data.Year + '. ' + response.data.Plot + ' Genre: ' + response.data.Genre + ' IMDB rating: ' + response.data.imdbRating + ' Production: ' + response.data.Production
                    // app.movieInfoResults.Title = response.data.Title;
                    app.movieInfoResults = response.data;
                })
                .catch(function (error) {
                  app.movieInfoResults = "Not a movie";
                })
        },
        addToMovieList: function(todo) {
          this.movieListTitle = this.movieInfoResults.Title;
        }
      },
    }


</script>
<style lang="scss">
  .movie-list-container {
    margin: 0 auto;

    &__user {
      margin: 0 0 0 6%;
      padding-top: 20px;
    }
  }
  #lead-form {
    width: 40%;
    margin: 0px auto;
    // height: 100%;
    display: inline-block;
    padding-top: 40px;
    margin: 40px 0 0 6%;
    vertical-align: top;
    background: #4D6AEB;
    border-radius: 5px;
    padding: 20px;
    ::-webkit-input-placeholder { /* Chrome/Opera/Safari */
      color: #C3C3C3;
    }
    ::-moz-placeholder { /* Firefox 19+ */
      color: #C3C3C3;
    }
    :-ms-input-placeholder { /* IE 10+ */
      color: #C3C3C3;
    }
    :-moz-placeholder { /* Firefox 18- */
      color: #C3C3C3;
    }

    h1 {
      color: #BCC3F9;
    }
  }
  .search-input {
    // width: 100%;
    color: #FFFFFF;
    width: 90%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;
    background: transparent;
    border-bottom: 1px solid #BCC3F9;
    border-top: none;
    border-left: none;
    border-right: none;

    &:focus {
      outline: 0;
    }
  }
  button {
    font-size: 14px;
    background-color: white;
    appearance: none;
    border: none;
    padding: 3px 6px;
    cursor: pointer;

    &:hover {

    }

    &:focus {
      outline: none;
    }
  }
  .submit-button {
    display: inline-block;
  }
  #submit-form {
    position: relative;
    bottom: 3px;
    height: 46px;
    right: 5px;
    color: #000;
    background: transparent;
    text-transform: uppercase;
    font-size: 16px;
    font-weight: bold;
  }
  .movie-info {

    &__title {
      font-size: 22px;
      margin: 5px 0;
    }
    &__year {
      font-size: 22px;
      margin: 5px 0;
    }
    &__genre {
      display: block;
      font-size: 16px;
      margin: 5px 0;
    }
    &__rating {
      display: block;
      font-size: 16px;
      margin: 5px 0;
    }
    &__plot {
      display: block;
      font-size: 16px;
      margin: 5px 0;
    }
    &__production {
      display: block;
      font-size: 16px;
      margin: 5px 0;
    }
  }
  #addMovieToList{
    margin-top: 10px;
    float: right;
  }

  /* Forward */
.hvr-forward {
  display: inline-block;
  vertical-align: middle;
  -webkit-transform: perspective(1px) translateZ(0);
  transform: perspective(1px) translateZ(0);
  box-shadow: 0 0 1px rgba(0, 0, 0, 0);
  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  -webkit-transition-property: transform;
  transition-property: transform;
}
.hvr-forward:hover, .hvr-forward:focus, .hvr-forward:active {
  -webkit-transform: translateX(8px);
  transform: translateX(8px);
}
</style>
