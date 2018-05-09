<template>
  <nav>
    <div class="nav-wrapper">
      <div class="container">
        <router-link :to="{ name: 'Dashboard'}" class="brand-logo">Employee Manager</router-link>
        <ul class="right">
          <li v-if="isLoggedIn"><span class="email white-text">{{ currentUser }}</span></li>
          <li v-if="isLoggedIn"><router-link to="/">Dashboard</router-link></li>
          <li v-if="!isLoggedIn"><router-link to="/login">Login</router-link></li>
          <li v-if="!isLoggedIn"><router-link to="/register">Register</router-link></li>
          <li v-if="isLoggedIn"><button @click="logout" class="btn black">Logout</button></li>
        </ul>
        <a class="btn-floating btn-large halfway-fab">
          <router-link :to="{ name: 'NewEmployee' }">
            <i class="material-icons">add</i>
          </router-link>
        </a>
      </div>
    </div>
  </nav>
</template>

<script>
import firebase from 'firebase'

export default {
  name: 'Navbar',
  data() {
    return {
      isLoggedIn: false,
      currentUser: false
    }
  },
  created() {
    if(firebase.auth().currentUser) {
      this.isLoggedIn = true
      this.currentUser = firebase.auth().currentUser.email
    }
  },
  methods: {
    logout() {
      firebase.auth().signOut().then(() => {
        this.$router.go({ path: this.$router.path })
      })
    }
  }
}
</script>

<style>
.nav-wrapper {
  background: #000100;
}

.btn-floating {
  background: #94C5CC;
}

.email {
  padding-right: 10px;
}
</style>


