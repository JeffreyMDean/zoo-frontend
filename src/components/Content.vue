<script>
import axios from "axios";
import ZooIndex from "./ZooIndex.vue";
import ZoosNew from "./ZoosNew.vue";

export default {
  components: {
    ZooIndex,
    ZoosNew,
  },
  data: function () {
      return {
        zoos: [
        { id: 3, name: "Leopard", description: "spotted cat", image: "https://via.placeholder.com/150"},
        { id: 4, name: "Panther", description: "dark cat", image: "https://via.placeholder.com/300"},
      ],
    };
  },
  created: function () {
    this.handleIndexZoos();
  },
  methods: {
    handleIndexZoos: function () {
      axios.get("http://localhost:5000/animals.json").then((response) => {
        console.log("zoos index", response);
        this.zoos = response.data;
      });
    },
    handleCreateZoo: function (params) {
      axios
      .post("http://localhost:5000/animals.json", params)
      .then((response) => {
        console.log("zoos create", response);
        this.zoos.push(response.data);
      })
      .catch((error) => {
        console.log("zoos create error", error.response);
      });
    },
  },
};
</script>

<template>
  <main>
    <ZoosNew v-on:createZoo="handleCreateZoo" />
    <ZooIndex v-bind:zoos="zoos" />
  </main>
</template>

<style></style>