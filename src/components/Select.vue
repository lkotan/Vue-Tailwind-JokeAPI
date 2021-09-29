<template>
  <select class="categories" @change="$emit('selectChange',$event.target.value)">
    <option disabled selected>Please Select Category</option>
    <option :value="category" v-for="category in categories" :key="category">{{
      category
    }}</option>
  </select>
</template>

<script>
export default {
  name: "Select",
  data() {
    return {
      categories: [
        "Programming",
        "Miscellaneous",
        "Dark",
        "Pun",
        "Spooky",
        "Christmas",
        "Any"
      ],
    };
  },
};
</script>

<style>
.categories {
  @apply w-64
    mb-4
    p-1
    rounded-md
    outline-none
    text-lg
    bg-gray-800;
}
</style>
