<template>
  <body>
    <div>
      <p>Your movie is : {{info}}</p>
    </div>
  </body>
</template>
<script src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="crossorigin="anonymous"></script>
<script type="text/javascript">
import axios from 'axios';
var randomMovieArray = ['Game of Thrones', 'Harry Potter', 'Lord of the Rings', 'Star Wars'];
var randomNumber = Math.floor((Math.random() * randomMovieArray.length - 1) + 1);
var randomMovie = randomMovieArray[randomNumber];
export default {
      name: 'movie-list',
      data () {
        return {
          info: ''
        }
      },
      mounted () {
        axios
        .get('http://www.omdbapi.com/?t=' + encodeURI(randomMovie) + '&apikey=991cf08e')
        .then(response => (this.info = response.data.Title))
        .catch(error => console.log(error))
      }
    }


</script>
