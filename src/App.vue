<template>
  <div id="app">
  <github-user-followers></github-user-followers>
  </div>
</template>

<script>


import GithubUserFollowers from "@/components/GetUserFollowers";
export default {
  name: 'app',
  components: {
    GithubUserFollowers
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 5px;
}
</style>
