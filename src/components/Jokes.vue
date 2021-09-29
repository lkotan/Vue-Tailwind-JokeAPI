<template>
  <div class="jokes">
    <Joke v-for="item in jokes" :key="item.id" :item="item" />
  </div>
</template>

<script>
import Joke from "./Joke.vue";
export default {
  name: "Jokes",
  props: {
    jokes: {
      type: Array,
    },
  },
  components: {
    Joke,
  },
};
</script>

<style>
.jokes{
    @apply

    w-7/12
}
</style>
