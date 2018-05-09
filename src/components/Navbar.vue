<template>
  <nav>
    <div class="nav-wrapper">
      <div class="container">
        <router-link :to="{ name: 'Dashboard'}" class="brand-logo">Employee Manager</router-link>
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
export default {
  name: 'Navbar',
  data() {
    return {

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
</style>


