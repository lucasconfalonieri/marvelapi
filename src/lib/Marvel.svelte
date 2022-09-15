<script>
import { each } from "svelte/internal";
import Loader from "./Loader.svelte"

let value = ''
let bool = false
let response = undefined

//1cd5500ac7310055a0b4e7cf26cb966ed1b260a634c9c1442470bdb9db39fc70ad4560712
const handleInput = (event) => value = event.target.value
$: if(bool == true) {
        fetch(`https://gateway.marvel.com:443/v1/public/characters?ts=1&name=${value}&apikey=4c9c1442470bdb9db39fc70ad4560712&hash=03916a218bb8756faeb9a57aeb81676d`)
        .then(res => res.json())
        .then(apiResponse =>{
            response = apiResponse.data.results || []
            bool = false
            console.log(response)
        },)
}

function validar(){
    bool = true
}



</script>

<input 
required
placeholder="Buscar personaje..."
value = {value} 
on:input={handleInput} 
/>

<button type= "submit" id="submit" on:click={validar}>Buscar </button>
<br><small> Por ejemplo: Hulk </small>

{#if bool}
    <Loader></Loader>
{:else}
    {#if response && response.length > 0}
        {#each response as personaje}
        <div>
            <h3>
                <strong>{personaje.name}</strong>
            </h3> 
        </div>
        <div>
            <h2>
                {personaje.description}
            </h2> 
        </div>
            <article>
                <img alt = {personaje.comics} src = {personaje.thumbnail.path}.{personaje.thumbnail.extension}/>
            </article>     
        {/each}
    {/if}
    {#if response}
        <div>
            <br><strong>Sin resultados</strong>
        </div>  
    {/if}
{/if}






