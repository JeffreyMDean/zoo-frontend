<script>
export default {
  props: {
    zoos: Array,
  },
};
</script>

<template>
  <div>
    <h1>All animals</h1>
    <div v-for="zoo in zoos" v-bind:key="zoo.id">
      <h2>{{ zoo.name }}</h2>
      <p>{{ zoo.description }}</p>
      <img v-bind:src="zoo.url" />
    </div>
  </div>
</template>

<style></style>