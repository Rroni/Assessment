<template>
  <div id="app">
    <GamesTable />
  </div>
</template>
ß
<script>
import GamesTable from "@/components/GamesTable.vue"
export default {
  name: 'App',
  components: {
    GamesTable
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
  margin-top: 60px;
}
</style>
