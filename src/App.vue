<script setup>
import HelloWorld from './components/HelloWorld.vue'

</script>

<template>
  <div>
    <a href="https://www.cuc.ac.cr/" target="_blank">
      <img src="https://www.cuc.ac.cr/wp-content/uploads/2022/12/logo-cuc.svg" class="logo" alt="CUC logo" />
    </a>
  </div>

  <div id="nav">
      <router-link to="/">Inicio</router-link>
   </div>

   <router-view></router-view> 

</template>

<script>
    export default {
      name: 'App'
    };
  </script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
.category-container{
  border: 1px solid yellow;
  padding: 50px;
}

.search-input{
  border: none;
  border-bottom: 1px solid yellow;
  min-height: 20px;
  margin-top: 20px;
  margin-bottom: 20px;
}

* {
  font-family: monospace;
}
</style>