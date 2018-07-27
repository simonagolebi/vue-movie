<template lang="html">
  <div class="login">
    <h3>Sign In</h3>
    <input type="text" v-model="email" placeholder="Email"><br>
    <input type="password" v-model="password" placeholder="Password"><br>
    <button v-on:click="signIn">Login</button>
    <p>You don't have an account? You can <router-link to="/sign-up">create one</router-link></p>
  </div>

</template>

<script>
import firebase from 'firebase';

export default {
  name: 'login',
  data: function() {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    // login: function() {
    //   this.$router.replace('/')
    // }
    signIn: function() {
      firebase.auth().signInWithEmailAndPassword(this.email, this.password).then(
        (user) => {
          this.$router.replace('home');
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
  .login {
    margin: 40px auto;
    text-align: center;
  }
  input {
    width: 300px;
    padding: 10px 18px;
    font-size: 18px;
    margin: 15px 0 0 0;
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
    margin-top: 20px;
    width: 10%;
    cursor: pointer;
    color: #ffffff;
    background: #84A2D5;
    border: none;
    outline: none;
    padding: 7px 5px;
    font-weight: bold;
    text-transform: uppercase;
    border-radius: 3px;

    &:hover {
      border: none;
    }
  }
  p {
    margin-top: 40px;
    font-size: 13px;
  }
  p a {
    text-decoration: underline;
    cursor: pointer;
  }
</style>
