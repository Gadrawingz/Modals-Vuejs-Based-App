<template>
  <h2>{{ pageTitle }}</h2>
  <Modal :header="header" :text="text" theme="sale"/>
</template>

<script>
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    Modal
  },

  data() {
    return {
      pageTitle: "Welcome to 1st App",
      header: "signup form!",
      text: "Grab your bag and go to vue school!"
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
