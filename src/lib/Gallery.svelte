<script lang="ts">
import { Images } from "svelte-images";
import { createClient } from '@supabase/supabase-js'
import {onMount} from 'svelte'
const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiYW5vbiIsImlhdCI6MTYyMzQxNzIwMiwiZXhwIjoxOTM4OTkzMjAyfQ.Lo86msAQIX432Z_-WZ6FwWenuntY6R4INjqVlePMM1s'

const SUPABASE_URL = "https://qhlvntmxjwhevzfkqjfs.supabase.co"

const supabase = createClient(SUPABASE_URL, SUPABASE_KEY)

let dataCarousel = []

////Funciones para el carousel
//Conectar a la Tabla Carousel
onMount(()=>{
      getdataCarousel()
})
async function getdataCarousel(){
  await supabase
  .from('Carousel')
  .select().then((res)=>{
       dataCarousel = res.data
  })
 
}
//buscar Cliente en la tabla Carousel

let clienteInput = ""
$: filterClienteCarousel = _.where(dataCarousel, {Cliente: clienteInput}); 
// filtrar de la tabla solo los valores de src, genera una lista con las direcciones
$: filterClienteImage =      _.pluck(filterClienteCarousel, 'src');  
// Si no se llama images la bd, no funciona el plugin
// Agregar a la lista de images el par key value src:
$: images = _.map(filterClienteImage, function(x){ return {src: x}; });
  
</script>
<div class="container">
       <header>
           <h1 id='title'>Planos de Impresión</h1>           
       </header>    

<!-- Corousel  -->

    <div id='leerDatosCarousel'>
           <p id='leerDatosCarousel'>Galería</p>
            <div class='form-input'>
               <label id='clientePlanos'>Cliente:</label>
               <input bind:value={clienteInput} placeholder='Nombre del Cliente' id='clienteInput' required class='form-input-size' />
              
                             
            </div>              
           <Images {images} gutter={5} numCols={2}/>  
    </div>              
    
</div>


<style>
  html{
    font-size: 16px;
}

body{
    background-color: rgba(98, 95, 241, 0.635);
    margin: 0;
    font-family: sans-serif;
    color: white;
}

.container{
  width: 100%;
  margin: 3.2rem auto 0 auto;
}

@media(min-width: 576px){
  .container{
    max-width: 540px;
  }
}

@media(min-width: 768px){
  .container{
    max-width: 720px
  }
}

header{
    text-align: center;
    margin-bottom: 1.5rem;
}

h1{
  font-weight: 400;
}

#leerDatosCarousel{
  color: white;
  font-size: 20px;
  text-align: center;
  font-weight: 200;
  font-style: italic;
  text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.5);
  background: rgba(21, 20, 85, 0.7);
  padding-bottom: 0.3rem;
  border-radius: 0.3rem;
 
}


#listaDatos{
  color: white;
  font-size: 20px;
  text-align: left;
  font-weight: 200;
  font-style: italic;
  text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.5);
  background: rgba(21, 20, 85, 0.7);
  padding-bottom: 0.3rem;
  border-radius: 0.3rem;
 
}
.form-input{
   margin: 0 2.5rem 1.2rem 2rem;
   text-align: left;
}

.form-input-size{
   display: block;
   width: 95%;
   height: 1.5rem;
   padding: 0.3rem 0.4rem;
   border-radius: 0.2rem;
   outline: 0;
   border-style: none;
   margin-top: 0.4rem;  
}

label {
 display: flex;
 align-items: center;
 font-size: 1.125rem;
 margin-bottom: 0.5rem;
}

button{
  
 width: 30%;
 padding: 0.7rem;
 background: rgb(7, 173, 7);
 color: white;
 border-radius: 0.2rem;
 cursor: pointer;
 border: none;
}
.one{
  list-style: square inside;
  padding-left: 2rem;
}
</style>
