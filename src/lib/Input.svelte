<script>
let value = ''
let bool = false
//1cd5500ac7310055a0b4e7cf26cb966ed1b260a634c9c1442470bdb9db39fc70ad4560712
const handleInput = (event) => value = event.target.value
$: if(bool == true) {
    fetch(`https://gateway.marvel.com:443/v1/public/characters?ts=1&name=${value}&apikey=4c9c1442470bdb9db39fc70ad4560712&hash=03916a218bb8756faeb9a57aeb81676d`)
    .then(res => res.json())
    .then(apiResponse =>{
        console.log(apiResponse.data.results[0])
    })
    bool = false
}
function validar(){
    bool = true
}

</script>

<input value = {value} on:input={handleInput} />

<button on:click={validar}>Buscar </button>



