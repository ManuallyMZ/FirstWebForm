<template>
  <SignUpForm />
</template>

<script>
import SignUpForm from './components/SignUpForm'

export default {
  name: 'App',
  components: {
    SignUpForm
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
body {
  margin: 0;
  background: #666666;
}
</style>
