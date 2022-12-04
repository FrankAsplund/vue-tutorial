<script>
export default {
  name: "Delete",
  props: {
    title: {
      type: String,
    },
  },

  methods: {
    deleteButton() {
      console.log("delete");
    },
  },
};
</script>

<template>
  <main>
    <button class="track-button" @click="deleteButton()">{{ title }}</button>
  </main>
</template>

<style scoped>
.track-button {
  font-size: 15px;
  font-weight: bold;

  background-color: rgb(255, 0, 0);
  border-style: none;
  border-radius: 10px;
  height: 30px;
  width: 80px;
  align-items: center;
  margin-left: 20px;
  margin-top: 10px;
}
</style>
