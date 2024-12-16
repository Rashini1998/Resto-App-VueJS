<template>
  <router-view/>
  <!-- <SignUp/> -->
</template>

<script>

export default {
  name: 'App',

  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
.body{
  padding: 0;
  margin: 0;
}
.logo {
    width: 100px;
    justify-items: center;
}

.register input, .login input, .addResto input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid purple;
}

.register button, .login button, .addResto button {
    width: 320px;
    height: 40px;
    border: 1px solid purple;
    color: white;
    background: purple;
    cursor: pointer;
    font-size: 14px;
    text-align: center;
}
</style>
