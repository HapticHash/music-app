<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title"> {{ current.title }} - <span> {{ current.artist }} </span> </h2>
        <div class="controls">
          <button class="prev" @click="prev"><i class="fas fa-step-backward"></i></button>
          <button class="play" v-if="!isPlaying" @click="play"><i class="fas fa-play"></i></button>
          <button class="pause" v-else @click="pause"><i class="fas fa-pause"></i></button>
          <button class="next" @click="next"><i class="fas fa-step-forward"></i></button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing': 'song'">
          {{ song.title }} - {{ song.artist }}
        </button>
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
        src: require('./assets/Justin_Bieber_Yummy_Official_Video_.mp3')
      },
      {
        title: 'How Long',
        artist: 'Charlie Puth',
        src: require('./assets/Charlie_Puth_quot_How_Long_quot_Official_Video_.mp3')
      },
      {
        title: 'Intensions',
        artist: 'Justin Bieber',
        src: require('./assets/Justin_Bieber_Intentions_Official_Video_Short_.mp3')
      },
      {
        title: 'Sunflower',
        artist: 'Post Malone',
        src: require('./assets/Post_Malone_Swae_Lee_Sunflower_Spider_Man_Into_the_Spider_Verse_.mp3')
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

      this.player.play();
      this.player.addEventListener('ended', function() {
        this.index++;
        if(this.index > this.songs.length-1) {
          this.index = 0;
        }

        this.current = this.songs[this.index];
        this.play(this.current);  
      }.bind(this));
      this.isPlaying = true;
    },

    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.songs.length -1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
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
* {
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
	color: #FFF;
}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.song-title {
  color: #53565A;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
  margin-top: 5vh;
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
  /* opacity: 0.8; */
  -webkit-box-shadow: 0 10px 20px 0 rgba(0, 0, 0, 0.19), 0 6px 6px 0 rgba(0, 0, 0, 0.23);  /* Safari 3-4, iOS 4.0.2 - 4.2, Android 2.3+ */
  -moz-box-shadow: 0 10px 20px 0 rgba(0, 0, 0, 0.19), 0 6px 6px 0 rgba(0, 0, 0, 0.23);  /* Firefox 3.5 - 3.6 */
  box-shadow: 0 10px 20px 0 rgba(0, 0, 0, 0.19), 0 6px 6px 0 rgba(0, 0, 0, 0.23);  /* Opera 10.5, IE 9, Firefox 4+, Chrome 6+, iOS 5 */
}
.play, .pause {
  font-size: 20px;
  font-weight: 700;
  padding: 45px;
  margin: 0px 15px;
  border-radius: 50%;
  color: #FFF;
  background-color: #021B79;
}
.next, .prev {
  font-size: 16px;
  font-weight: 700;
  padding: 30px;
  margin: 0px 15px;
  border-radius: 50%;
  color: #FFF;
  background-color: #0575E6;
}
.playlist {
  padding: 0px 30px;
  margin-top: 2vh;
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
  color: #1A2980;
}
.playlist .song.playing {
  color: #FFF;
  background-image: linear-gradient(to right, #1A2980, #26D0CE);
}
.fas {
  font-size: 2em;
}
</style>
