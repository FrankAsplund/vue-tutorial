<template>
  <div class="submit-form">
    <div v-if="!submitted">
      <div class="form-group">
        <label for="title">Title</label>
        <input
          type="text"
          class="form-control"
          id="title"
          required
          v-model="playlist.title"
          name="title"
        />
      </div>

      <div class="form-group">
        <label for="artist">Artist</label>
        <input
          class="form-control"
          id="artist"
          required
          v-model="playlist.artist"
          name="artist"
        />
      </div>

      <button @click="savePlaylistCard" class="btn">Submit</button>
    </div>

    <div v-else>
      <h4>You submitted successfully!</h4>
      <button class="btn" @click="newPlaylistCard">Add</button>
    </div>
  </div>
</template>

<script>
import DataService from "../services/DataService";

export default {
  name: "add-playlistCard",
  data() {
    return {
      playlist: {
        id: null,
        title: "",
        artist: "",
        published: false,
      },
      submitted: false,
    };
  },
  methods: {
    savePlaylistCard() {
      var data = {
        title: this.playlist.title,
        artist: this.playlist.artist,
      };

      DataService.create(data)
        .then((response) => {
          this.playlist.id = response.data.id;
          console.log(response.data);
          this.submitted = true;
        })
        .catch((e) => {
          console.log(e);
        });
    },

    newPlaylistCard() {
      this.submitted = false;
      this.playlist = {};
    },
  },
};
</script>

<style>
.submit-form {
  max-width: 300px;
  margin: auto;
}
</style>
