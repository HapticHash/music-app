<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title"> {{ current.title }} - <span> {{ current.artist }} </span> </h2>
        <div class="contro">
          <button class="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next">Next</button>
        </div>
      </section>
      <section class="playlist">

      </section>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [{
        title: 'Yummy Yummy',
        artist: 'Justin Bieber',
        src: './assets/Justin_Bieber_Yummy_Official_Video_.mp3'
      }],
      player: new Audio()
    }
  },
  methods: {
    play(song) {
      if(typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    }
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    //this.player.play();
  }

}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}

</style>
