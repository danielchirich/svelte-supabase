<script>
    
    export let userbase
    export let user
    export let initPromise
    export let pagina
    let username, password, email
    function signUp() {
        initPromise = userbase.signUp({username, password, email})
            .then((u) => user = u)
    }
</script>
<div class='container'>
  <form on:submit|preventDefault={signUp}>
    <div class="login">
               <h2>Registrarse - Iniciar Sesión</h2>        
    </div>
    <br/>
     <div class='form-input'>
               <button on:click={() => pagina = 'signin'}>Iniciar sesion</button>
     </div>

    <div class='form-input'>
              <label id='username'>Username</label>
              <input label="Username" bind:value={username} type="text" required class='form-input-size'/>
    </div>
    <div class='form-input'>
              <label id='password'>Password</label>
              <input label="Password" bind:value={password} type="password" required class='form-input-size'/>
    </div>
    <div class='form-input'>
              <label id='email'>Email</label>
              <input label="Email" bind:value={email} type="email" required class='form-input-size'/>
    </div>
    <div class='form-input'>    
    
             <button>Registrarse!</button>
    </div>
  </form>
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


header{
    text-align: center;
    margin-bottom: 1.5rem;
}

h1,h2{
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

.form-input{
   margin: 0 2.5rem 1.2rem 2rem;
   text-align: center;
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

</style>

  





