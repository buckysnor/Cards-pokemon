<template>



    <div class="pokemon-card-container">

    <div class="pokemon-card">

        <div class="fundo">
        <img v-bind:src="(`https://pokeres.bastionbot.org/images/pokemon/${pokemon.id}.png`)"    class="image">  
    </div>


        <div class="content">
        <h1 class="nome-do-pokemon"><strong>{{name | upper}}</strong></h1>
        <span class="tipo-do-pokemon"> {{pokemon.tipo}} </span>


     <div class="especialidade">

        <p> <strong> ALTURA: {{pokemon.altura }}cm  </strong>      </p>
        <p> <strong>PESO: {{pokemon.peso}}kg </strong>       </p>
        <p> <strong>HABILIDADE:   {{pokemon.habilidade}} </strong></p>
        <p></p>
        <p></p>
        
     </div>

        <h1 class="pokemon-logo"> </h1>
        </div>
    </div>

</div>


</template>



<script>
import axios from 'axios';

export default  {
    created: function(){

   axios.get(this.url).then(res => {
       console.log(res.data);

    this.pokemon.tipo = res.data.types[0].type.name;
    this.pokemon.peso = res.data.weight;
    this.pokemon.altura = res.data.height;
    this.pokemon.habilidade = res.data.abilities[0].ability.name;
    this.pokemon.id = res.data.id;
        console.log(this.pokemon);
    })    

},
    data(){
        return{
            pokemon:{
            tipo:'',
            altura:'',
            peso:'',
            id:''
            // createPokeImage:''
}
        }
    },


    props:{
        num:Number,
        name:String,
        url:String

    },

 filters: {   
     upper: function(value) {
         var newName = value[0].toUpperCase() + value.slice(1);
         return newName;
     }
 }

}



</script>





<style>



</style>

