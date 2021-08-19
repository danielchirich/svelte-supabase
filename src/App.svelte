<script>
import Aplication from './lib/Aplication.svelte';

import { createClient } from '@supabase/supabase-js'
import {onMount} from 'svelte'
import SignUp from './routes/SignUp.svelte'
import SignIn from './routes/SignIn.svelte'

    

  
    let user = null
    const userbase = window.userbase
    let initPromise = userbase.init({appId: '2dfbe303-6941-462f-8464-8cc701f7f954'})
        .then((session) => user = session.user)
    
    function signOut() {
        initPromise = userbase.signOut()
            .then(() => user = null)
    }
    let pagina = 'signup'
    
</script>

<div class="container">
   <div class='login'>
    {#await initPromise}       
        Esperando conexión...
    {:then _}
        {#if user}              
                 <Aplication/>                                             
                     
        {:else}
            {#if pagina === 'signup'}
                <SignUp {userbase} bind:user bind:initPromise bind:pagina />
            {:else if pagina === 'signin'}
                <SignIn {userbase} bind:user bind:initPromise bind:pagina />            
            {/if}
            
        {/if}
        
    {/await}
    
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

.login{
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


</style>

  





