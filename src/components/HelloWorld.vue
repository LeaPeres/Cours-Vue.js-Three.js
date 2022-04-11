<template>
  <div class="container">
  <!--
    <button v-on:click="show = !show">Permutter texte</button>
    <transition name="fade">
      <p v-if="show">bonjour</p>
    </transition>

    <button v-on:click="isActive = !isActive">Permutter image</button>
      <transition>
        <p v-if="isActive"><img id="image1" src="../assets/logo.png"/></p>
        <p v-if="!isActive"><img id="image2" src="../assets/test.jpg"/></p>
      </transition>
      
    <br /><br />
-->
  <img id="logo_pokemon" src="../assets/pokemon-logo.png" alt="logo pokemon"/>
  <h1>Attrapez-les tous !</h1>
  <label><b>Entre un numéro de 1 à 898 et observe quel Pokémon sauvage apparaît :</b></label>
  <br/> <br/>
  <input id='recherche' type='text' v-on:change='recherchepk'>
    <table class='tableau_pokemon'>
      <tr>
        <th>Id</th>
        <th>Nom</th>
        <th>Image</th>
        <th>Type(s)</th>
      </tr>
      <tr>
        <th>{{this.id}}</th>
        <th><h2>{{this.nom}}</h2></th>
        <th><img id="src"/></th>
        <th>
          <ul>
            <li v-for='value in this.type'>
              {{value.type.name}}
            </li>
          </ul>  
        </th>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data () {
    return{
    show : true,
    isActive : true,
    info:null,
    nom:null,
    image:null,
    type:null,
    id:null,
    }
  },
  methods: {
    logg: function () {
      console.log("press")
    },
    recherchepk: function(){
      var i = document.getElementById('recherche').value

    axios
      .get('https://pokeapi.co/api/v2/pokemon/' + i)
      .then(response => {
        this.info = response
        this.nom = response.data.name
        this.image = response.data.sprites.front_default
        this.type = response.data.types
        this.id = response.data.id
        document.getElementById('src').src = this.image 
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
#app{
    margin-top:0px!important;
}

.container{
  background-color:#FFCC01;
  padding:30px;
}

#logo_pokemon{
  width:20vw;
}

input{
    border-radius: 20px;
    background-color: #D62620;
    border: none;
    padding: 10px;
    width: 25%;
    text-align: center;
    font-size: 18px;
    font-weight: 800;
    color: #ffffff;
}

.tableau_pokemon{
  width: 100%;
  justify-content: center;
  align-items: center;
  margin-top: 5em;
  border-collapse: collapse;
  color:#ffffff;
}

th{
  border: solid 1px #ffffff;
  background-color: #3262AD
}

h2{
  text-transform: uppercase;
  text-decoration:underline;
  font-size:14px;
}

ul{
  margin: 0px;
  padding: 0px;
}

li{
  list-style-type: none;
}
</style>