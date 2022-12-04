<template>
  <div class="list row">
    <div class="col-md-8">
      <div class="input-group mb-3">
        <input
          type="text"
          class="form-control"
          placeholder="Search by title"
          v-model="title"
        />
        <div class="input-group-append">
          <button
            class="btn btn-outline-secondary"
            type="button"
            @click="searchTitle"
          >
            Search
          </button>
        </div>
      </div>
    </div>
    <div class="col-md-6">
      <h4>Playlist</h4>
      <ul class="list-group">
        <li
          class="list-group-item"
          :class="{ active: index == currentIndex }"
          v-for="(playlist, index) in playlists"
          :key="index"
          @click="setActivePlaylist(playlist, index)"
        >
          {{ playlist.title }}
        </li>
      </ul>

      <button class="m-3 btn btn-sm btn-danger" @click="removeAllPlaylists">
        Remove All
      </button>
    </div>
    <div class="col-md-6">
      <div v-if="currentPlaylist">
        <h4>Playlist</h4>
        <div>
          <label><strong>Title:</strong></label> {{ currentPlaylist.title }}
        </div>
        <div>
          <label><strong>Artist:</strong></label> {{ currentPlaylist.artist }}
        </div>
        <div>
          <label><strong>Status:</strong></label>
          {{ currentPlaylist.published ? "Published" : "Pending" }}
        </div>

        <router-link to="/add" class="nav-link">Add</router-link>

        <router-link
          :to="'/playlist' + currentPlaylist.id"
          class="badge badge-warning"
          >Edit</router-link
        >
      </div>
      <div v-else>
        <br />
        <p>Please click on a PLaylist...</p>
      </div>
    </div>
  </div>
</template>

<script>
import DataService from "../services/DataService";

export default {
  name: "playlists-list",
  data() {
    return {
      playlists: [],
      currentPlaylist: null,
      currentIndex: -1,
      title: "",
    };
  },
  methods: {
    retrievePlaylists() {
      DataService.getAll()
        .then((response) => {
          this.playlists = response.data;
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },

    refreshList() {
      this.retrievePlaylists();
      this.currentPlaylist = null;
      this.currentIndex = -1;
    },

    setActivePlaylist(playlist, index) {
      this.currentPlaylist = playlist;
      this.currentIndex = playlist ? index : -1;
    },

    removeAllPlaylists() {
      DataService.deleteAll()
        .then((response) => {
          console.log(response.data);
          this.refreshList();
        })
        .catch((e) => {
          console.log(e);
        });
    },

    searchTitle() {
      DataService.findByTitle(this.title)
        .then((response) => {
          this.playlists = response.data;
          this.setActivePlaylist(null);
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
  mounted() {
    this.retrievePlaylists();
  },
};
</script>

<style>
.list {
  text-align: left;
  max-width: 750px;
  margin: auto;
}

@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
