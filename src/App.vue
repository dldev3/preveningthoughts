<template>
  <div id="app">
    <full-page :options="options" id="fullpage" v-if="isLoaded">
      <div
        v-for="preveningThought in preveningThoughts"
        :key="preveningThought.data.id"
        class="section"
      >
        <div class="container">
          <img src="./assets/shower.png" alt="prevening icon" />

          <div class="quote-symbol">❝</div>
          <p class="quote">
            <a target="_blank" :href="preveningThought.data.url">{{ preveningThought.data.title }}</a>
          </p>
          <div class="quote-symbol">❞</div>
          <div class="details">
            <div class="details-author">Author: {{ preveningThought.data.author_fullname }}</div>
            <div
              class="stats"
            >{{ preveningThought.data.ups }} upvotes | {{ preveningThought.data.num_comments }} Comments</div>
          </div>
        </div>
      </div>
      <!-- ❝❞ -->
    </full-page>

    <div class="quote-symbol section container" v-else>
      <loading-spinner></loading-spinner>
    </div>
  </div>
</template>

<script>
import LoadingSpinner from "./components/LoadingSpinner.vue";

export default {
  name: "App",
  components: {
    LoadingSpinner
  },
  created() {
    fetch("https://www.reddit.com/r/Showerthoughts.json?limit=20")
      .then(response => response.json())
      .then(data => {
        this.preveningThoughts = data.data.children;
        this.preveningThoughts.shift();
        this.isLoaded = true;
      });
  },
  data() {
    return {
      isLoaded: false,
      preveningThoughts: [],
      options: {
        scrollBar: true,
        sectionsColor: [
          "#41b883",
          "#ff5f45",
          "#0798ec",
          "#fec401",
          "#1bcee6",
          "#ee1a59",
          "#2c3e4f",
          "#ba5be9",
          "#b4b8ab",
          "#41b883",
          "#ff5f45",
          "#0798ec",
          "#fec401",
          "#1bcee6",
          "#ee1a59",
          "#2c3e4f",
          "#ba5be9",
          "#0798ec",
          "#0798ec",
          "#fec401"
        ]
      }
    };
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Knewave&display=swap");

#app {
  font-family: sans-serif;
  color: #2d3748;
}

body {
  margin: 0;
  padding: 0;
}

h3 {
  margin: 0;
}

.container {
  margin: auto;
  max-width: 800px;
  padding: 80px 16px;
}

.section {
  text-align: center;
}

.quote-symbol {
  font-size: 64px;
  line-height: 0;
  margin-top: 50px;
  color: white;
}

.quote a {
  text-decoration: none;
  font-family: "Knewave", cursive;
  color: white;
  font-size: 36px;
  line-height: 1.5;
}

.quote a:hover {
  color: #edf2f7;
}

.details {
  margin-top: 2rem;
}
.details-stats {
  margin-top: 4px;
}
</style>
