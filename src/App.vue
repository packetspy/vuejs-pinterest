<template>
  <div id="app">
    <div class="container">
      <div class="button-wrapper">
        <button class="btn" @click="searchUnsplash('Autumn')">Autumn</button>
      </div>
    </div>
  </div>
</template>

<script>
//import HelloWorld from "./components/HelloWorld.vue";

import Axios from "axios";
import { Stack, StackItem } from "vue-stack-grid";

export default {
  name: "app",
  components: {
    Stack,
    StackItem
  },
  data: () => ({
    images: []
  }),
  methods: {
    searchUnsplash(topic) {
      this.images = [];
      Axios.get(
        `https://api.unsplash.com/search/photos?query=${topic}&per_page=20`,
        {
          headers: {
            Authorization: "Client-ID <YourAccessKeyGoesHere>",
            "Accept-Version": "v1"
          }
        }
      )
        .then(response => {
          this.images = response.data.results;
        })
        .catch(() => {
          this.images = [];
        });
    }
  }
};
</script>

<style>
.container {
  width: 80vw;
  margin: 0 auto;
}
.button-wrapper {
  display: flex;
  justify-content: center;
  margin-bottom: 25px;
}
.bt {
  font-size: 18px;
  background-color: #42b983;
  color: white;
  padding: 10px 20px;
}
</style>
