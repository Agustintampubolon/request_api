<template>
  <div id="app">
    <div
      class="text-5xl text-center header h-64 flex justify-center items-center"
    >
      <h4 class="text-muted">Lyrics of a Song</h4>
    </div>
    <h6 class="text-center text-muted">retrieve the lyrics of a song</h6>
    <div>
      <form @submit.prevent="searchLyrics" class="text-center pt-4">
        <div class="col-md-12">
          <input
            v-model="title"
            type="text"
            placeholder="Masukkan Judul Lagu"
            class="pt-1"
          />
          <input
            v-model="artist"
            type="text"
            placeholder="Masukkan Nama Artis"
            class="pt-1"
          />
        </div>
        <br />
        <button type="submit" class="btn btn-primary text-white">Search</button>
      </form>
    </div>
    <br />
    <div class="card mb-3">
      <div class="row no-gutters">
        <div class="col-md-12">
          <div class="card-body">
            <h4 class="card-title" style="text-align: center !important">
              {{ title }}
            </h4>
            <template>
              <p class="card-text" style="text-align: center !important">
                Dipopulerkan oleh : {{ artist }}
              </p>
              <p class="card-text" style="text-align: center !important">
                {{ lyrics }}
              </p>
            </template>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      artist: "coldplay",
      title: "paradise",
      lyrics: [],
    };
  },

  async created() {
    try {
      const response = await this.$axios.get(`v1/${this.artist}/${this.title}`);
      const data = await response;
      // console.log(data.data);
      this.lyrics = data.data.lyrics;
      // console.log(this.lyrics);

      this.artist = "";
      this.title = "";
    } catch (error) {
      console.log(error);
    }
  },

  methods: {
    async searchLyrics() {
      try {
        const response = await this.$axios.get(
          `v1/${this.artist}/${this.title}`
        );
        const data = await response;

        this.artist = "";
        this.title = "";

        // console.log(data.data);
        this.lyrics = data.data.lyrics;
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style scoped></style>
