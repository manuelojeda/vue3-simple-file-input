<template>
  <file-input v-model="file" />
</template>

<script>
import FileInput from './components/FileInput'

export default {
  name: 'App',
  components: {
    FileInput
  },
  data () {
    return {
      file: null
    }
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
