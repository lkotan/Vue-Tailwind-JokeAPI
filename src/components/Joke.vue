<template>
  <div class="joke">
    <header>
      <h1>{{ item.category.toUpperCase() }}</h1>
      <Flags :flags="flags" />
    </header>
    <section class="content">
      <div v-if="!item.joke" class="">
        <p class="setup">{{ item.setup }}</p>
        <p class="delivery">{{ item.delivery }}</p>
      </div>
      <div v-else>
        <p>{{ item.joke }}</p>
      </div>
    </section>
  </div>
</template>

<script>
import Flags from "./Flags.vue";
export default {
  name: "Joke",
  props: {
    item: {
      type: Object,
    },
  },
  components: {
    Flags,
  },
  computed: {
    flags() {
      return Object.entries(this.item.flags).map((x) => x);
    },
  },
};
</script>

<style>
.joke {
  @apply my-3
    p-4
    rounded-md
    cursor-pointer
    bg-gray-900
    hover:bg-gray-700
    duration-200;
}
.joke header {
  @apply flex
  justify-between
  items-center
  my-3;
}
.joke header h1 {
  @apply text-indigo-300
    font-semibold;
}

.joke .content {
  @apply my-2;
}
.joke .content div:first-child {
  @apply flex
    items-center
    text-lg;
}
.joke .content .setup {
  @apply mr-6
    text-gray-400;
}
</style>
