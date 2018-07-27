<template lang="html">
  <div class="sign-up">
    <h3>Create a new account!</h3>
    <div class="sign-up-form">
      <input type="text" v-model="email" placeholder="Email">
      <input type="password" v-model="password" placeholder="Password">
      <button v-on:click="signUp">Sign Up</button>
    </div>
    <span>or go back to <router-link to="/login">login</router-link></span>
  </div>
</template>

<script>
import firebase from 'firebase';

export default {
  name: 'SignUp',
  data: function() {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    signUp: function() {
      firebase.auth().createUserWithEmailAndPassword(this.email, this.password).then(
        (user) => {
          this.$router.replace('hello');
        },
        (err) => {
          alert('Oops. ' + err.message);
        }
      )
    }
  }
}
</script>

<style scoped lang="scss">
  .sign-up {
    margin: 40px auto;
    text-align: center;
  }
  input {
    width: 300px;
    padding: 10px 18px;
    font-size: 18px;
    margin: 15px auto;
    display: block;
    background: #ffffff;
    border: 2px solid #6921bc;
    border-radius: 3px;

    &:focus {
      outline: 0;
    }
  }
  input:-webkit-autofill {
    -webkit-box-shadow: 0 0 0 30px white inset;
  }
  button {
    width: 10%;
    cursor: pointer;
    display: block;
    text-align: center;
    margin: 20px auto;
    color: #ffffff;
    background: #84A2D5;
    border: none;
    outline: none;
    padding: 7px 5px;
    font-weight: bold;
    text-transform: uppercase;
    border-radius: 3px;
  }
  span {
    display: block;
    margin-top: 20px;
    font-size: 11px;
  }
</style>
