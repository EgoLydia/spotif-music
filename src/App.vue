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
const player = new Audio();

const pause = () => {
  player.pause();
  isPlaying.value = false;
};

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
header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}

main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}

.song-title {
  color: #53565a;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title span {
  font-weight: 400;
  font-style: italic;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}

button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}

button:hover {
  opacity: 0.8;
}

.play,
.pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: #cc2e5d;
}

.next,
.prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background-color: #ff5858;
}

.playlist {
  padding: 0px 30px;
}

.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}

.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.playlist .song:hover {
  color: #ff5858;
}

.playlist .song.playing {
  color: #fff;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
}
</style>
