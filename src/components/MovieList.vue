<template>
  <body>
    <div class="movie-list-container">
      <!-- <img src="../assets/film.svg" class="movie-list-container__icon"> -->
      <!-- <p>Your movie is : {{info}}</p> -->
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
      </form>
      <!-- <button v-on:click="logout">Logout</button> -->
    </div>
  </body>
</template>
<script src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="crossorigin="anonymous"></script>
<script type="text/javascript">
import axios from 'axios';
import firebase from 'firebase';
import $ from 'jquery';
// var randomMovieArray = ['Game of Thrones', 'Harry Potter', 'Lord of the Rings', 'Star Wars'];
// var randomNumber = Math.floor((Math.random() * randomMovieArray.length - 1) + 1);
// var randomMovie = randomMovieArray[randomNumber];

export default {
      name: 'movie-list',
      // compiled(){
      //   $.on('navigation.hide', () => this.show = false)
      //   $.on('navigation.show', () => this.show = true)
      // },
      data () {
        return {
          info: '',
          findMovie: '',
          movieInfoResults: '',
          // show: true
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
                  app.movieInfoResults = "Not a movie"
                })
        },
        // logout: function() {
        //   firebase.auth().signOut().then(() => {
        //     this.$router.replace('login')
        //   })
        // }
      },
      // mounted () {
      //   axios
      //   .get('http://www.omdbapi.com/?t=' + encodeURI(randomMovie) + '&apikey=991cf08e')
      //   .then(response => (this.info = response.data.Title))
      //   .catch(error => console.log(error))
      // }
    }
    $( "#submit-form" ).click(function() {
      $( ".movie-info" ).slideDown( "slow");
    });

</script>
<style lang="scss">
  .movie-list-container {
    position: absolute;
    margin: 0 auto;
    width: 100%;
    height: 430px;
    background: linear-gradient(225deg, #FFA807, #f9b027, #fcbd46);
    background: -webkit-linear-gradient(225deg, #FFA807, #f9b027, #fcbd46);
    animation: GradientAnimation 20s ease infinite;
    -webkit-animation: GradientAnimation 20s ease infinite;
    @keyframes GradientAnimation {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }

@-webkit-keyframes GradientAnimation {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }
    &__icon {
      height: 420px;
      position: absolute;
      opacity: 0.2;
      left: 0px;
      z-index: 0;
      bottom: 30px;
      transform: skewX(-9deg);
    }
  }
  #lead-form {
    width: 800px;
    margin: 40px auto;
    height: 100%;
  }
  .search-input {
    // width: 100%;
    width: 758px;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;
    border: 2px solid #FFE68E;

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
      background: #ffffff;
      border: 2px solid #6921bc;
      color: #000000;
    }

    &:focus {
      outline: none;
    }
  }
  .submit-button {
    display: inline-block;
  }
  #submit-form {
    border: 2px solid #FFE68E;
    position: relative;
    bottom: 3px;
    height: 46px;
    right: 5px;
    color: #a0edff;
    background: #27C4E8;
    text-transform: uppercase;
    font-size: 12px;
    font-weight: bold;
  }
  .movie-info {
    &__title {
      font-size: 22px;
    }
    &__year {
      font-size: 22px;
    }
    &__genre {
      display: block;
      font-size: 16px;
    }
    &__rating {
      display: block;
      font-size: 16px;
    }
    &__plot {
      display: block;
      font-size: 16px;
    }
    &__production {
      display: block;
      font-size: 16px;
    }
  }
</style>
