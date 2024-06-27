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
      axios.get("http://localhost:5000/animals.json").then((response) => {
        console.log("zoos index", response);
        this.zoos = response.data;
      });
    },
    handleCreateZoo: function (params) {
      const formData = new FormData();
      formData.append('name', params.name);
      formData.append('description', params.description);
      formData.append('image', params.image);
      console.log(formData);
      axios
      .post("http://localhost:5000/animals.json", formData)
      .then((response) => {
        
        console.log("zoos create", response.data);
        this.zoos.push(response.data);
      })
      .catch((error) => {
        console.log("zoos create error", error.response);
      });
    },
    handleShowZoo: function (zoo) {
      console.log("handleShowzoo", zoo);
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