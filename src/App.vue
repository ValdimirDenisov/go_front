<template>
  <goBoard :size="9"/>    
</template>

<script>
import goBoard from './components/goboard.vue'

export default {
  name: 'App',
  components: {
    goBoard
  }
}
</script>

<style>

</style>
