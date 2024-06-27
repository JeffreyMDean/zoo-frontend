<script>
import axios from "axios";
import ZooIndex from "./ZooIndex.vue";
import ZoosNew from "./ZoosNew.vue";
import Modal from "./Modal.vue";
import ZooShow from "./ZooShow.vue";

export default {
  components: {
    ZooIndex,
    ZoosNew,
    ZooShow,
    Modal,
  },
  data: function () {
      return {
        zoos: [
        { id: 3, name: "Leopard", description: "spotted cat", image: "https://via.placeholder.com/150"},
        { id: 4, name: "Panther", description: "dark cat", image: "https://via.placeholder.com/300"},
      ],
      currentZoo: {},
      isZoosShowVisible: false,

    };
  },
  created: function () {
    this.handleIndexZoos();
  },
  methods: {
    handleIndexZoos: function () {
      axios.get("http://localhost:5000/zoos.json").then((response) => {
        console.log("zoos index", response);
        this.zoos = response.data;
      });
    },
    handleCreateZoo: function (params) {
      axios
      .post("http://localhost:5000/zoos.json", params)
      .then((response) => {
        console.log("zoos create", response);
        this.zoos.push(response.data);
      })
      .catch((error) => {
        console.log("zoos create error", error.response);
      });
    },
    handleShowZoo: function (zoo) {
      console.log("handleShowPhoto", zoo);
      this.currentZoo = zoo;
      this.isZoosShowVisible = true;
    },
    handleClose: function () {
      this.isZoosShowVisible = false; 
    },
  },
};
</script>

<template>
  <main>
    <ZoosNew v-on:createZoo="handleCreateZoo" />
    <!-- <ZooIndex v-bind:zoos="zoos" /> -->
    <ZooIndex v-bind:zoos="zoos" v-on:showZoo="handleShowZoo" />
    <Modal v-bind:show="isZoosShowVisible" v-on:close="handleClose">
      <h1>Test</h1> 
      <ZooShow v-bind:zoo="currentZoo" />
    </Modal>
  </main>
</template>

<style></style>