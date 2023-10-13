<template>
  <div class="bgimg">
      <div class="container">
  <NavComp/>
  <router-view></router-view>
  </div>
  </div>
   
  
</template>

<script>
import NavComp from './components/Navigations.vue'

export default {
  name: 'App',
  components: {
    NavComp
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
  margin: -10px;
  padding: 0;
}

.container {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
.bgimg {
  background-image: url(./img/nba.jpg);
  height: 100vh;
}
</style>
