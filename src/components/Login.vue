<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col s12 m8 offset-m2">
          <div class="login card-panel white-text center">
            <h3>Login</h3>
            <form action="index.html">
              <div class="input-field">
                <i class="material-icons prefix">email</i>
                <input type="email" id="email" v-model="email" placeholder="Email Address">
              </div>
              <div class="input-field">
                <i class="material-icons prefix">lock</i>
                <input type="password" id="password" v-model="password" placeholder="Password">
              </div>
              <button @click.prevent="login" class="btn btn-large btn-extended grey lighten-4 black-text">Login</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import firebase from 'firebase'

export default {
  name: 'Login',
  data() {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    login() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(user => {
          alert(`U r logged in as ${user.email}`)
          this.$router.go({ path: this.$router.path })
        })
    }
  }
}
</script>

<style>
.login {
  background: #66B3BA;
}
</style>

