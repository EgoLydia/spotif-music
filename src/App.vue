<script setup lang="ts">
</script>

<template>
  <div id="app">
    <header>
      <h1>Spotif - Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }} - <span>{{ current.artiste }}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button v-for="song in songs" :key="song.src" @click="play(song)"
          :class="song.src === current.src ? 'song-playing' : 'song'">
          {{ song.title }} - {{ song.artiste }}
        </button>
      </section>
    </main>
  </div>
</template>

const isPlaying = ref(false);

</template>
const current = ref({});

const index = ref(0);

const songs = ref([
  {
    title: " Electricity",
    artiste: "Pheelz Ft Davido",
    src: import('./assets/Pheelz_Ft_Davido_-_Electricity.mp3')
  },
  {
    title: "Soso",
    artiste: "Omah Lay",
    src: import('./assets/Omah_Lay_-_Soso.mp3')
  },
]);
const next = () => {
  index.value++;
  if (index.value > songs.value.length - 1) {
    index.value = 0;
  }

  current.value = songs.value[index.value];
  play(current.value);
};

const prev = () => {
  index.value--;
  if (index.value > 0) {
    index.value = songs.value.length - 1;
  }

  current.value = songs.value[index.value];
  play(current.value);
};
<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
