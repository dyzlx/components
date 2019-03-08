<template lang="pug">
  div#app
    div#nav
      router-link(to="/about") About
      router-link(to="/textarea") Textarea
    router-view
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
