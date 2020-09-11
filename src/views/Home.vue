<template>
  <div class="home">
    <v-btn @click="miseAJour()">MAJ</v-btn>
    <div class="test">
      <span>
        <img v-if="tailleNombre < 7" src="../../../images/vide.png" width="10%"/>
        <img v-if="tailleNombre < 6" src="../../../images/vide.png" width="10%"/>
        <img v-if="tailleNombre < 5" src="../../../images/vide.png" width="10%"/>
        <img v-if="tailleNombre < 4" src="../../../images/vide.png" width="10%"/>
        <img v-if="tailleNombre < 3" src="../../../images/vide.png" width="10%"/>
        <img v-if="tailleNombre < 2" src="../../../images/vide.png" width="10%"/>
        <img v-if="tailleNombre < 1" src="../../../images/vide.png" width="10%"/>
      </span>
      <span class="compteur" v-for="element in tableau" :key="element">
        
        <img v-if="element === '../../../images/1.png'" src="../../../images/1.png" width="10%"/>
        <img v-if="element === '../../../images/2.png'" src="../../../images/2.png" width="10%"/>
        <img v-if="element === '../../../images/3.png'" src="../../../images/3.png" width="10%"/>
        <img v-if="element === '../../../images/4.png'" src="../../../images/4.png" width="10%"/>
        <img v-if="element === '../../../images/5.png'" src="../../../images/5.png" width="10%"/>
        <img v-if="element === '../../../images/6.png'" src="../../../images/6.png" width="10%"/>
        <img v-if="element === '../../../images/7.png'" src="../../../images/7.png" width="10%"/>
        <img v-if="element === '../../../images/8.png'" src="../../../images/8.png" width="10%"/>
        <img v-if="element === '../../../images/9.png'" src="../../../images/9.png" width="10%"/>
        <img v-if="element === '../../../images/0.png'" src="../../../images/0.png" width="10%"/>
      </span>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
export default {
  data(){
    return{
      nombre: 0,
      tailleNombre: 0,
      tableau: [],
      tableau2: []
    }
  },
  name: 'Home',
  mounted(){
    axios.get("http://" + window.location.hostname + ":3000/url").then(resp => {
      console.log(resp)
      this.nombre = resp.data
      this.tailleNombre = resp.data.toString().length
      this.miseEnTab(resp.data)
      setInterval(this.miseAJour, 5000);
    })
  },
  methods:{
    miseEnTab(data){
      console.log("oui");
      console.log(this.tailleNombre)
      for(let i=0; i<data.toString().length; i++){
        console.log(this.nombre.toString()[i]);
        this.tableau.push("../../../images/"+data.toString()[i]+".png")
      }
    },
    miseAJour(){
      this.tableau = []
      axios.get("http://" + window.location.hostname + ":3000/url").then(resp => {
      console.log(resp)
      if(this.nombre != resp.data){ // on a eu un passage en plus (mini)
        this.playSound('http://soundbible.com/mp3/Air%20Plane%20Ding-SoundBible.com-496729130.mp3')
      }
      this.nombre = resp.data
      this.tailleNombre = resp.data.toString().length
      this.miseEnTab(resp.data)
    })
    },
    playSound (sound) {
      if(sound) {
        var audio = new Audio(sound);
        audio.play();
      }
    }
  }

}
</script>
<style>
.test{
  margin-left: 25%;
  margin-top: 15%;
  /*
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);*/
}
.v-application{
  background-image: url("../assets/fond.png") !important;
  background-repeat: no-repeat;
  background-size: 100% 100% !important;
}
</style>
