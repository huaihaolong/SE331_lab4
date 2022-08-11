<template>
  <div id="div-choose" v-for="size in totalevents" :key="size">
    <router-link :to="{ path: '/', query: { pagesize: size } }">{{
      size
    }}</router-link>
  </div>
  <nav>
    <router-link :to="{ name: 'EventList' }">Home</router-link> |
    <router-link :to="{ name: 'about' }">About</router-link>
  </nav>
  <router-view />
</template>

<script>
import EventService from '@/services/EventService.js'
import { watchEffect } from '@vue/runtime-core'
export default {
  name: 'App',
  data() {
    return {
      totalevents: 0
    }
  },
  created() {
    watchEffect(() => {
      EventService.getTotalEvents()
        .then((response) => {
          let data = response.data
          this.totalevents = data.length
        })
        .catch((error) => {
          console.log(error)
        })
    })
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
h4 {
  font-size: 20px;
}

#div-choose {
  float: flex;
  margin: 1px;
  text-align: center;
  background-color: aquamarine;
}
</style>
