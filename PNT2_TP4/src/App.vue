<template>
  <div id="app" class="container-fluid my-3">
    <div class="jumbotron jumbotron-fluid">
      <h1>TP4</h1>
      <Navbar />
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
export default {
  name: "App",
  components: {
    Navbar,
  },
};
</script>

<style>
.jumbotron {
    color: black;
    /* background-color:darkgrey; */
    text-align: center;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}


</style>
