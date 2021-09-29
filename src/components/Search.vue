<template>
  <div class="search">
    <input
      type="text"
      placeholder="Search..."
      @keyup="$emit('searchEvent', $event.target.value)"
    />
  </div>
</template>

<script>
export default {
  name: "Search",
 
};
</script>

<style>
.search input {
  @apply w-80
    py-1 px-2
    mb-4
    border-2
    rounded-lg
    border-gray-200
    outline-none
    focus:border-purple-400
    text-black
    font-bold
    tracking-widest
    duration-500;
}
</style>
