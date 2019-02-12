<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
  }
}

  fetch("http://www.madeinblue.com/wp-json/wp/v2/posts").then(function(response) {
      var contentType = response.headers.get("content-type");
      if(contentType && contentType.indexOf("application/json") !== -1) {
          return response.json().then(function(json) {
              // traitement du JSON
              console.log(json);
          });
      } else {
          console.log("Oops, nous n'avons pas du JSON!");
      }
  });
</script>
