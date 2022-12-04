<script>
import Delete from "./Delete.vue";

export default {
  components: {
    Delete,
  },

  name: "Card",
  props: {
    title: {
      type: String,
    },
    length: {
      type: String,
    },

    trackId: {
      type: String,
    },
    starId: {
      type: String,
    },
  },
};
</script>

<!-- ☆ -->
<template>
  <div class="container">
    <div class="track-container">
      <div class="track-title">{{ title }}</div>

      <div class="rate">
        <input type="radio" id="star5" name="rate" value="5" />
        <label for="star5" title="text">5 stars</label>
        <input type="radio" id="star4" name="rate" value="4" />
        <label for="star4" title="text">4 stars</label>
        <input type="radio" id="star3" name="rate" value="3" />
        <label for="star3" title="text">3 stars</label>
        <input type="radio" id="star2" name="rate" value="2" />
        <label for="star2" title="text">2 stars</label>
        <input type="radio" id="star1" name="rate" value="1" />
        <label for="star1" title="text">1 star</label>
      </div>

      <div class="track-length">{{ length }}</div>
    </div>
    <Delete title="Delete" />
  </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.track-container {
  margin-top: 10px;
  padding: 10px;
  align-items: center;
  display: flex;

  border-style: none;
  background-color: rgba(112, 128, 144, 0.14);
  border-radius: 10px;
  width: 350px;
  height: 50px;
}

.track-container:hover {
  background-color: rgba(255, 0, 0, 0.195);
}

.track-title {
  font-size: 15px;
  margin-right: 10px;
}

.track-length {
  margin-left: 15px;
}

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

.rate {
  float: left;
  align-items: center;
  padding: 0 10px;
}
.rate:not(:checked) > input {
  position: absolute;
  top: -9999px;
}
.rate:not(:checked) > label {
  float: right;
  width: 1em;
  overflow: hidden;
  white-space: nowrap;
  cursor: pointer;
  font-size: 20px;
  color: #ccc;
}
.rate:not(:checked) > label:before {
  content: "★ ";
}
.rate > input:checked ~ label {
  color: #ffc700;
}
.rate:not(:checked) > label:hover,
.rate:not(:checked) > label:hover ~ label {
  color: #deb217;
}
.rate > input:checked + label:hover,
.rate > input:checked + label:hover ~ label,
.rate > input:checked ~ label:hover,
.rate > input:checked ~ label:hover ~ label,
.rate > label:hover ~ input:checked ~ label {
  color: #c59b08;
}
</style>
