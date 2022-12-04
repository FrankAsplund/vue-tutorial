<template>
  <div v-if="currentPlaylist" class="edit-form">
    <h4>Playlist</h4>
    <form>
      <div class="track-container">
        <label for="title">Title</label>
        <input
          type="text"
          class="form-control"
          id="title"
          v-model="currentPlaylist.title"
        />
      </div>
      <div class="form-group">
        <label for="artist">Artist</label>
        <input
          type="text"
          class="form-control"
          id="artist"
          v-model="currentPlaylist.artist"
        />
      </div>

      <div class="form-group">
        <label><strong>Status:</strong></label>
        {{ currentPlaylist.published ? "Published" : "Pending" }}
      </div>
    </form>

    <button
      class="badge badge-primary mr-2"
      v-if="currentPlaylist.published"
      @click="updatePublished(false)"
    >
      UnPublish
    </button>
    <button
      v-else
      class="badge badge-primary mr-2"
      @click="updatePublished(true)"
    >
      Publish
    </button>

    <button class="badge badge-danger mr-2" @click="deletePlaylist">
      Delete
    </button>

    <button type="submit" class="badge badge-success" @click="updatePlaylist">
      Update
    </button>
    <p>{{ message }}</p>
  </div>

  <div v-else>
    <br />
    <p>Please click on a Playlist...</p>
  </div>
</template>

<script>
import DataService from "../services/DataService";
import axios from "axios";

export default {
  name: "playlist",
  data() {
    return {
      currentPlaylist: null,
      message: "",
    };
  },
  methods: {
    getPlaylist(id) {
      DataService.get(id)
        .then((response) => {
          this.currentPlaylist = response.data;
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },

    updatePublished(status) {
      var data = {
        id: this.currentPlaylist.id,
        title: this.currentPlaylist.title,
        artist: this.currentPlaylist.artist,
        published: status,
      };

      DataService.update(this.currentPlaylist.id, data)
        .then((response) => {
          console.log(response.data);
          this.currentPlaylist.published = status;
          this.message = "The status was updated successfully!";
        })
        .catch((e) => {
          console.log(e);
        });
    },

    updatePlaylist() {
      DataService.update(this.currentPlaylist.id, this.currentPlaylist)
        .then((response) => {
          console.log(response.data);
          this.message = "The playlist was updated successfully!";
        })
        .catch((e) => {
          console.log(e);
        });
    },

    deletePlaylist() {
      DataService.delete(this.currentPlaylist.id)
        .then((response) => {
          console.log(response.data);
          this.$router.push({ name: "playlists" });
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
  mounted() {
    this.message = "";
    this.getPlaylist(this.$route.params.id);
  },
};
</script>

<style>
.edit-form {
  max-width: 300px;
  margin: auto;
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
</style>
