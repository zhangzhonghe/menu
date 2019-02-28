<template>
  <div id="app">
    <Menu @open="onOpen" animation/>
  </div>
</template>

<script>
import Menu from './components/Menu.vue'

export default {
  name: 'app',
  components: {
    Menu
  },
  methods: {
    onOpen (e) {
      console.log(e.active)
    }
  }
}
</script>

<style>
  * {
    margin: 0;
  }  
</style>
