<template>
  <div id="App">
   <header>
    <h1>My Music</h1>
   </header>
   <main>
    <section class="player">
      <h2 class="song-title">{{ current.title }}-
       <span>{{ current.artist }}</span>
      </h2>
      <div id="control">
        <button class="prev"> Prev. </button>
        <button class="play" v-if="!isPlaying" @click="play">Play</button>
        <button class="pause" v-else  @click="pause">Pause</button>
        <button class="next">Next</button>
      </div>
    </section>
    <section class="playlist">
      <h3> The playlist</h3>
      <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src)? 'song playing':'song '">{{ song.title }} - {{ song.artist }}</button>

    </section>
   </main>
  </div>
  
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      current:{},
      index:0,
      isPlaying: false,
      songs:[
        {
          title: 'Greatful',
          artist:'Neffex',
          src: require('./assets/neffex-grateful.mp3')
        },
        {
          title:'Invincible',
          artist:'Deaf Kev',
          src: require('./assets/deaf-kev-invincible.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods:{
    play(song)
    {
      if(typeof song.src !=='undefined'){
        this.current=song;
        this.player.src =this.current.src;
      }
      this.player.play();
      this.isPlaying=true;
   },
   pause(){
    this.player.pause();
    this.isPlaying= false;
   }  
 },
  created(){
    this.current= this.songs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  }

}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  font-family: sans-serif;
}
header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #FFF;
}
.prev {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 15px 32px;
  border-radius: 250px 0px 0px 250px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  transition-duration: 0.4s;
  cursor: pointer;
}
.play , .pause {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 15px 32px;
  border-radius: 10px 10px 10px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  transition-duration: 0.4s;
  cursor: pointer;
}
.next {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 15px 32px;
  border-radius: 0px 500px 500px 0px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  transition-duration: 0.4s;
  cursor: pointer;
}
</style>