<script>
export default {
  props: {
    zoo: Object,
  },
};
</script>

<template>
  <div>
    <h1>Zoo information</h1>
    <p>Name: {{ zoo.name }}</p>
    <p>Description: {{ zoo.description }}</p>
    <p>Image: {{ zoo.image }}</p>
    
  </div>
</template>

<style></style>