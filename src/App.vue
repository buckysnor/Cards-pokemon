<template>
  <div id="app">
<div class="caixa"> 
<input class="pesquisa1" type="pesquisa" placeholder="POKEBUSCA" v-model="busca">

<div v-for="(poke,index) in resultadoBusca" :key="index">


<Pokemon :name="poke.name"  :url="poke.url" :num="index+1" />
<Global />
<Header />
 
 
  </div>
  </div>

  </div>
</template>

<script>

import axios from 'axios';
import Pokemon from './components/Pokemon';
import Global from './components/Global.css';
import Header from './components/Header';

export default {
  name:'App',

data(){
  return{
    pokemons:[],
    imagens:[],
  busca:''
 }
},

created:function(){
  axios.get("https://pokeapi.co/api/v2/pokemon?limit=150&offset=0").then(res=> {
    console.log(res.data.results);
    this.pokemons = res.data.results;


    
  
  })


//  axios.get("https://pokeres.bastionbot.org/images/pokemon/25.png").then(teste =>{
//       console.log(teste.data);
//       this.imagens = teste.data;
//       console.log(this.imagens);
      

//  })


},

components:{
  Pokemon,
  Global,
  Header 
},

computed:{
  resultadoBusca:function(){
    if(this.busca == ''|| this.busca == ' '){
      return this.pokemons;
    }else{
      return this.pokemons.filter(pokemon => pokemon.name == this.busca);
    }
    }
  }


}

</script>

<style>




</style>
