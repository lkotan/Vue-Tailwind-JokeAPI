<template>
  <div class="flags">
    <div v-for="flag in flags" :key="flag[0]">
      <h3 v-if="flag[1]">{{ flag[0] }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: "Flags",
  props: {
    flags: {
      type: Array,
    },
  },
};
</script>

<style>
.joke .flags {
  @apply flex;
}
.joke .flags h3 {
  @apply ml-3
    py-1 px-3
    rounded-full
    bg-indigo-600
    text-white
    text-sm
    font-bold;
}
</style>
