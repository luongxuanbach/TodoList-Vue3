<template>
  <Header/>
  <div id="app">

  </div>
  <Todos/>
</template>

<script>
import Header from "@/components/Header";
import Todos from "@/components/Todos";
export default {
  name: 'App',
  components: {Todos, Header},
}
</script>
<style>
#app{
  font-family: Avenir, Helvetica, sans-serif;
}
</style>