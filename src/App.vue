<template>
  <div id="app">
    <Navbar />
    <div class="app-content">
      <router-view />
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
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.container {
  width: 90%;
  margin: 0 auto;
}

#app {
  height: 100vh;
  background-image: url("./assets/captain-america.png");
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: top 50px right;
}

.app-content {
  width: 60%;
  margin-top: 50px;
  background-color: #ffffffb3;
  border-radius: 20px;
}

@media (max-width: 1000px) {
  .app-content {
    width: 90%;
  }

  #app {
    background-image: none;
  }
}

@media (max-width: 650px) {
  .app-content {
    width: 100%;
  }
}
</style>
