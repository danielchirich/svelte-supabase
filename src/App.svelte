<script>

import { createClient } from '@supabase/supabase-js'
import {onMount} from 'svelte'
const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiYW5vbiIsImlhdCI6MTYyMzQxNzIwMiwiZXhwIjoxOTM4OTkzMjAyfQ.Lo86msAQIX432Z_-WZ6FwWenuntY6R4INjqVlePMM1s'

const SUPABASE_URL = "https://qhlvntmxjwhevzfkqjfs.supabase.co"

const supabase = createClient(SUPABASE_URL, SUPABASE_KEY)
let alldata = []

onMount(()=>{
      getdata()
})
async function getdata(){
  await supabase
  .from('Pagos')
  .select().then((res)=>{
       alldata = res.data
  })
 
}
let datanueva = [
		{ cliente: '' ,
			cantidad: '',
			descripcion: '',
			importe: ''  }]

async function cargarDatos() {
  try{
    await supabase
    .from('Pagos')
    .insert(datanueva)
  }
  catch(err){
      console.log(err)
  }  
}
let id = ''
let cliente = ''
let cantidad = ''
let descripcion = ''
let importe = ''
async function deleteDatos(id) {
  
    await supabase
    .from('Pagos')
    .delete().match({ id: id })}

async function upsertDatos(id,cliente,cantidad,descripcion,importe) {
  
    await supabase
    .from('Pagos')
    .upsert({ id: id, cliente: cliente, cantidad: cantidad, descripcion: descripcion, importe: importe })}


$: alldataPluckImporte = _.pluck(alldata, 'importe')
$: alldataPluckImporteSuma =  _.reduce(alldataPluckImporte, function(memo, num){ return memo + num; }, 0)


let cliente_busqueda = ''
$: alldataWhereCliente = _.where(alldata, {cliente: cliente_busqueda});
$: alldataPluckImporteCliente = _.pluck(alldataWhereCliente, 'importe')
$: alldataPluckImporteSumaCliente =  _.reduce(alldataPluckImporteCliente, function(memo, num){ return memo + num; }, 0)


</script>

<div class="container">
       <header>
           <h1 id='title'>Svelte Supabase app</h1>           
       </header>

    <div id='cargarDatos'>
      <p id='cargarDatos'>Cargar Datos</p>

      {#each datanueva as data}
          <div class='form-input'>
               <label id='cliente'>Cliente</label>
               <select bind:value={data.cliente} id='cliente' class='form-input-size' required >
                   <option disabled selected value>Seleccione Cliente</option>
                   <option value='Coyamel SA'>Coyamel SA</option>
                   <option value='Jorge Luis Tolosa SA'>Jorge Luis Tolosa SA</option>
                   <option value='Autopartes Argenta SA'>Autopartes Argenta SA</option>
                   <option value='Synertech SA'>Synertech SA</option>
                   <option value='Piccione Cristian'>Piccione Cristian</option>
               </select>
           </div>
      
           <div class='form-input'>
              <label id='cantidad'>Cantidad</label>
              <input type=number  bind:value={data.cantidad} placeholder="Cantidad" id='cantidad'                 class='form-input-size' required> 
          </div>
          <div class='form-input'>
              <label id='descripcion'>Descripción</label>
              <input bind:value={data.descripcion} placeholder="Descripcion" id='descripcion'  class='form-input-size' required>
          </div>
         <div class='form-input'>
              <label id='importe'>Importe</label>
              <input type=number bind:value={data.importe} placeholder="Importe" id='importe'                 class='form-input-size' required>
         </div>
      {/each}

         <div class='form-input'>
              <button on:click={cargarDatos}>Cargar Datos</button>
         </div>
    </div>
<br/>
   <div id='borrarDatos'>
             <p id='borrarDatos'>Borrar Datos</p>
    <div class='form-input'>
              <label id='id'>Descripción</label>
              <input bind:value={id} placeholder="id delete" id='descripcion' class='form-input-size' required>
    </div>
    <div class='form-input'>
             <button on:click={deleteDatos(id)}>Borrar</button>
    </div>
    
  </div>
<br/>
    <div id='modificarDatos'>
              <p id='modificarDatos'>Modificar Datos</p>
          <div class='form-input'>
              <label id='id'>Id</label>
              <input bind:value={id} placeholder="id" id='id' class='form-input-size' required>
          </div>
          <div class='form-input'>
              <label id='cliente'>Cliente</label>
              <input bind:value={cliente} placeholder="cliente" id='cliente' class='form-input-size'>
          </div>
          <div class='form-input'>
              <label id='cliente'>Cantidad</label>
              <input type=number bind:value={cantidad} placeholder="cantidad" id='cantidad' class='form-input-size'>
          </div>
          <div class='form-input'>
              <label id='descripcion'>Descripción</label>
              <input bind:value={descripcion} placeholder="descripcion" id='descripcion' class='form-input-size'>
          </div>
          <div class='form-input'>
              <label id='importe'>Importe</label>
              <input type=number bind:value={importe} placeholder="importe" id='importe' class='form-input-size'>
          </div>
          <div class='form-input'>
              <button on:click={upsertDatos(id,cliente,cantidad,descripcion,importe)}>Modificar</button>
          </div>
    </div>   

      
    <div id='leerDatos'>
           <p id='leerDatos'>Leer Datos</p>
            <div class='form-input'>
               <label id='cliente'>Cliente a buscar</label>
               <select bind:value={cliente_busqueda} id='cliente' class='form-input-size' required >
                   <option disabled selected value>Seleccione Cliente</option>
                   <option value='Coyamel SA'>Coyamel SA</option>
                   <option value='Jorge Luis Tolosa SA'>Jorge Luis Tolosa SA</option>
                   <option value='Autopartes Argenta SA'>Autopartes Argenta SA</option>
                   <option value='Synertech SA'>Synertech SA</option>
                   <option value='Piccione Cristian'>Piccione Cristian</option>
               </select>
          </div>
           
      {#each alldataWhereCliente as data} 
         
          <div class='form-input'>
                  <ul class="one">
                      <li>id: {data.id}* Cant.: {data.cantidad} * Desc.: {data.descripcion} * Imp.: {data.importe} </li>
                  </ul>             
         </div>
      {/each}  
        
         <div class='form-input'>  
              <p>Importe Total: {alldataPluckImporteSumaCliente}</p>
         </div>
       
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

#cargarDatos, #borrarDatos, #modificarDatos, #leerDatos{
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