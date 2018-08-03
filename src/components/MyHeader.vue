<template>
  <header class="vue-header">
    <div class="app-container__wrapper">
      <!-- <img src="../assets/film.svg" class="app-container__wrapper__icon"> -->
      <!-- <div class="app-container__wrapper__name">Movie-Vue</div> -->
    </div>
    <div class="app-container__wrapper__routes">
      <router-link to="/">Home</router-link>
      <!-- <router-link to="/towatchlist">Watch-List</router-link> -->
      <a v-on:click="logout">Logout</a>
    </div>
  </header>
</template>
<script type="text/javascript">
  import firebase from 'firebase';
  export default {
    methods : {
      logout: function() {
        firebase.auth().signOut().then(() => {
          this.$router.replace('login')
        })
      }
    }
  }
</script>
<style lang="scss">
  .vue-header {
    height: 50px;
    background: linear-gradient(to right, #FFA807, #f9b027, #fcbd46);
  }
  .app-container {

    h1 {
      text-transform: uppercase;
      font-size: 25px;
      margin-bottom: 10px;
      letter-spacing: 0.5px;
    }
    &__wrapper {
      position: relative;
      top: 6px;
      margin-left: 20px;
      display: inline-block;
      &__icon {
        display: inline-block;
        height: 35px;
        vertical-align: middle;
      }
      &__name {
        display: inline;
        vertical-align: middle;
        text-transform: uppercase;
        color: #ffffff;
      }
    }
    &__wrapper {
      &__routes {
        display: inline-block;
        float: right;
        position: relative;
        top: 17px;
        right: 20px;
        a {
          text-decoration: none;
          font-size: 12px;
          margin: 0 5px 0px 0;
          padding: 2px 5px;
          border-radius: 3px;
          cursor: pointer;
          text-transform: lowercase;
          color: #ffffff;

          &:hover{
            font-weight: bold;
          }

          &:last-child{
            margin-right: 0;
          }
        }
      }
    }
  }
  .router-link-exact-active {
    border: 2px solid #ffffff;
    padding: 2px 5px;
  }
</style>
