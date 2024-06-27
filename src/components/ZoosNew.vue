<script>
export default {
  data: function () {
    return { 
      newZooParams: {},
    };
  },
  methods: {
    handleSubmit: function () {
      this.$emit("createZoo", this.newZooParams);
      this.newZooParams = {};
    },
  },
};
</script>

<template>
  <div>
    <h1>New Zoo</h1>
    <form v-on:submit.prevent="handleSubmit">
      <div>
        Name:
        <input type="text" v-model="newZooParams.name" />
      </div>
      <div>
        Description:
        <input type="text" v-model="newZooParams.description" />
      </div>
      <div>
        Image:
        <input type="url" v-model="newZooParams.imageURL" />
      </div>
      <button type="submit">Create zoo</button>
    </form>
  </div>
</template>

<style></style>