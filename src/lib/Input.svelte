<script>
import { each } from "svelte/internal";
import personaje from './Personaje.svelte'

let value = ''
let bool = false
let response = []


//1cd5500ac7310055a0b4e7cf26cb966ed1b260a634c9c1442470bdb9db39fc70ad4560712
const handleInput = (event) => value = event.target.value
$: if(bool == true) {
    fetch(`https://gateway.marvel.com:443/v1/public/characters?ts=1&name=${value}&apikey=4c9c1442470bdb9db39fc70ad4560712&hash=03916a218bb8756faeb9a57aeb81676d`)
    .then(res => res.json())
    .then(apiResponse =>{
        response = apiResponse.data.results || []
    })
    bool = false
}
function validar(){
    bool = true
}

</script>

<input 
placeholder="Buscar personaje..."
value = {value} 
on:input={handleInput} 
/>

<button on:click={validar}>Buscar </button>

{#if bool}
    <strong>Loading...</strong>
{:else}
    {#if response.length > 0}
        {#each response as personaje}
        <div>
            <strong>{personaje.name}</strong>
        </div>
        <div>
            {personaje.description}
        </div>
            <article>
                <img alt = {personaje.description} src = {personaje.thumbnail.path}.{personaje.thumbnail.extension}/>
            </article>     
        {/each}
        {:else}
            <strong>Sin resultados</strong>
        {/if}
{/if}

<style>
    article{
        border: 1px solid #eee;
        border-radius: 4px;
        padding: 16px;
    }

</style>




