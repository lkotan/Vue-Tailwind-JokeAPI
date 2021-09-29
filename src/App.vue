<template>
  <div id="app">
    <h1 class="title">
      JokeAPI
      <a
        href="https://sv443.net/jokeapi/v2/"
        target="_black"
        title="Go To Documentation"
        >Documentation</a
      >
    </h1>
    <Select @selectChange="selectChange" />
    <Search @searchEvent="searchEvent" />
    <Jokes v-if="jokes.length != 0" :jokes="jokes" />
    <h2 v-else v-html="message"></h2>
  </div>
</template>

<script>
import Search from "@/components/Search";
import Jokes from "@/components/Jokes";
import Select from "@/components/Select";

export default {
  name: "App",
  components: {
    Search,
    Jokes,
    Select,
  },
  data() {
    return {
      jokes: [],
      message: null,
      search: null,
      category: null,
    };
  },
  methods: {
    getJokes(search, category) {
      let query = "https://v2.jokeapi.dev/joke";
      if (search == null && category == null) {
        fetch(`${query}/Any?amount=10`)
          .then((res) => res.json())
          .then((data) => (this.jokes = data.jokes));
      } else if (search != null) {
        if (category == null) {
          fetch(`${query}/Any?contains=${search}&amount=10`)
            .then((res) => res.json())
            .then((data) => {
              if (data.error) {
                this.message = `No match found with <b>${this.search.toUpperCase()} &#128532</b>`;
                this.jokes = [];
                return;
              }
              this.jokes = data.jokes;
            });
        } else {
          fetch(`${query}/${category}?contains=${search}&amount=10`)
            .then((res) => res.json())
            .then((data) => {
              if (data.error) {
                this.message = `No matches found for <b>${this.search.toUpperCase()} &#128532</b> in (<i>${category}</i>) `;
                this.jokes = [];
                return;
              }
              this.jokes = data.jokes;
            });
        }
      } else if (category != null) {
        fetch(`${query}/${category}?amount=10`)
          .then((res) => res.json())
          .then((data) => {
            this.jokes = data.jokes;
          });
      }
    },
    searchEvent(value) {
      this.search = value;
      this.getJokes(this.search, this.category);
    },
    selectChange(value) {
      this.category = value;
      this.getJokes(this.search, this.category);
    },
  },
  created() {
    this.getJokes(this.search, this.category);
  },
};
</script>

<style>
body {
  @apply bg-gradient-to-l
  from-blue-900
  to-black;
}
#app {
  @apply mt-8
  flex
  flex-col
  items-center
  text-white;
}

#app .title {
  @apply mb-3
  text-xl
  uppercase;
}
#app .title a {
  @apply text-indigo-300;
}
</style>
