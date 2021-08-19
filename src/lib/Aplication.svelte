<script>

import Pagos from './Pagos.svelte';
import Gallery from './Gallery.svelte';
import { Images } from "svelte-images";
import { createClient } from '@supabase/supabase-js'
import {onMount} from 'svelte'

let gallery = false;
let pagos = false;

</script>


       

    <div id='leerDatosCarousel'>
           
            <div class='form-input'>
             <br/>
              <label>
	              <input type=checkbox bind:checked={gallery}>
	               Galería de Planos
             </label>
            </div>
            <div class='form-input'>
             <label>
	              <input type=checkbox bind:checked={pagos}>
	              Estado de cuenta Clientes
            </label>             
            </div>                 
                         
            
    </div>              
    


{#if gallery}
     <!-- content here --><Gallery/>
{/if}

{#if pagos}
     <!-- content here --><Pagos/>
{/if}


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

  





