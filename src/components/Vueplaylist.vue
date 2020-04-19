<template>
  <div class="music">
   <header>
     <h1>My Music Player</h1>
   </header>
   <main>
     <section class="player">
       <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}
         </span></h2>
        <div class="controls">
         <button class="prev" @click="prev">Prev</button>
         <button class="play" v-if="!isPlaying" @click="play">Play</button>
         <button class="pause" v-else @click="pause">Pause</button>
         <button class="next" @click="next">Next</button>
        </div>
     </section>
     <section class="playlist">
       <h3>The Playlist</h3>
       <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src 
       == current.src) ? 'song playing' : 'song'">
       {{ song.title }} - {{ song.artist }}
       </button>
     </section>
  </main>
 </div>
</template>

<script>

export default {
  name: 'Vueplaylist',
  
  data (){
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
      title: 'Imagine',
      artist: 'John Lennon',
      src: require('../assets/imagine-JohnLennon.mp3')
        },
        {
      title: 'Heal the World',
      artist: 'Michael Jackson',
      src: require('../assets/Healtheworld-MichaelJackson.mp3')
        },
         {
      title: 'Four Strong Winds',
      artist: 'Neil Young',
      src: require('../assets/FourStrongWinds-NeilYoung.mp3')
        },
        {
      title: 'Cant Help Falling in Love',
      artist: 'Elvis Presley',
      src: require('../assets/CantHelpFallingInLove-ElvisPresley.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play (song) {
     if (typeof song.src != "undefined") {
       this.current = song;

       this.player.src = this.current.src;
     }
       this.player.play();
       this.player.addEventListener('ended', function () {
         this.index++;
         
         this.index++;
    if(this.index > this.songs.length -1) {
         this.index = 0;
    }
         this.current = this.song[this.index];
         this.play(this.current);
       
    }.bind(this));
    this.isPlaying = true;
    },

    pause () {
        this.player.pause();
        this.isPlaying = false;    
        },
    next () {
        this.index++;
        if (this.index > this.songs.length -1) {
            this.index = 0;
        }
        this.current = this.songs[this.index];
        this.play(this.current);
    },
    prev (){
        this.index--;
        if (this.index < 0) {
            this.index = this.songs.length -1;
        }
        this.current = this.songs[this.index];
        this.play(this.current);
    }  
   },

  created (){
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
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
  background-color: rgb(99, 0, 0);
  color: #fff;
}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 50px;
}

</style>
