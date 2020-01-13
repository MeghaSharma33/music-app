<template>
  <div id="app">
  <header>
    <h1>MUSICA</h1>
    </header>
  <main>
      <section class = "player">
          <h2 class="song-title">{{current.title}} - <span>{{current.artist}}</span></h2>
        <div class = "control">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play"> Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <div class="line"></div>
        <button v-for="song in songs" :key="song.src" @click="play(song)" 
                 :class="(song.src == current.src) ? 'song playing' : 'song'">
            {{song.title}} - {{song.artist}}

          </button>
      </section>  </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data: function() {
    return {
      current: {},
      index :0,
      isPlaying: false,
      songs: [
        {
          title: 'Takeaway',
          artist: 'The Chainsmokers',
          src: require('./assets/takeaway-chainsmokers.mp3')
        },
        {
          title: 'Memories',
          artist: 'Maroon 5',
          src: require('./assets/memories-maroon-5.mp3')
        },
        {
          title: 'Can We Kiss Forever',
          artist: 'Kina Ft Adriana Proenza',
          src: require('./assets/Kina - Can We Kiss Forever ft. Adriana Proenza.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods:{
     play (song) {
       if (typeof song.src !== "undefined") {
         this.current = song;

         this.player.src = this.current.src;

       }

       this.player.play();
       this.player.addEventListener('ended',function(){
          this.index++;
       if(this.index > this.songs.length -1){
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
       if(this.index > this.songs.length -1){
         this.index = 0;
       }
       this.current = this.songs[this.index];
       this.play(this.current);
       },
      prev(){
         this.index--;
       if(this.index < 0){
         this.index > this.songs.length -1;
        
       }
       this.current = this.songs[this.index];
       this.play(this.current);
      
     }       

  },
  created () {
    this.current = this.songs[this.index]
    this.player.src = this.current.src;
    // this.player.play();
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Monoton&display=swap');
@import url('https://fonts.googleapis.com/css?family=Fredericka+the+Great&display=swap');
@import url('https://fonts.googleapis.com/css?family=Galada&display=swap');
@import url('https://fonts.googleapis.com/css?family=Russo+One&display=swap');
* {

  margin:0;
  padding: 0;
  box-sizing: border-box;

}
body {
  background-image: linear-gradient(to right, salmon,pink);
  
}
header{
  display: flex;
  font-family:'Monoton', cursive;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-image: linear-gradient(to right, salmon,pink);
  color: #EE2F4C;

}

main {
  width: 100;
  max-width:700px;
  margin: 0 auto;
  padding: 40pxp;

}

.song-title{
  color:#87173E;
  font-size: 32px;
  font-family: 'Fredericka the Great', cursive;
  font-weight: 700;
  text-transform: uppercase;
  text-align:center;

}

.song-title span {
  font-weight: 400;
  font-style: italic;
}

.controls {
  display:flex;
  justify-content: center;
  padding: 30px 15px;


}
button{
  appearance: none;
  background:none;
  border:none;
  outline: none;
  cursor:pointer;
}
button:hover{
  opacity: 0.8;
}
.play,.pause{

  font-size: 20px;
  font-weight:700;
  padding:15px 25px;
  margin: 30px 50px;
  font-family: 'Galada', cursive;
  border-radius: 40%;
  color: black;
  background-color: tomato;

}

.next,.prev{
  font-size: 20px;
  font-weight:700;
  padding:15px 25px;
  margin: 30px 80px;
  font-family: 'Galada', cursive;
  border-radius: 40%;
  color: black;
  background-color:crimson;

}
.playlist{
  padding: 0px 30px;

}
.playlist h3{
  color:#87173E;
  font-size: 28px;
  font-weight:400;
  font-family: 'Russo One', sans-serif;
  margin-bottom: 30px;
  margin-top: 30px;
  text-align:center;
}

.playlist .song{
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor:pointer;
  color:#d64161;
}
.playlist .song:hover{
  color:crimson
}

.playlist .song.playing{
  color: white;
  background-image: linear-gradient(to right, #CC2E5D, #FF5858);
}

</style>
