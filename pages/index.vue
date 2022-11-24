<template>
    <div>

        <NuxtLink v-for="mountain in mountainsArray" class="mountain-name" :key="mountain" :to="`/about/${countryName}`">
                <p @click="getMountainName" >{{mountain}}</p>
            </NuxtLink>

    </div>
</template>

<script setup>
import { ref, onBeforeMount} from 'vue';

onBeforeMount(fetchData)

const countryName = ref('')

async function fetchData(){
    let mountains = []
    const response = await fetch('https://api.nuxtjs.dev/mountains')
    const data = await response.json()
    
    data.forEach(element => {
        mountains.push(element.slug)
    });
    return mountains
}


let mountainsArray = await fetchData()

function getMountainName(e){
    let selectedCountry = e.target
    countryName.value = selectedCountry.textContent
}



</script>

<style  scoped>

.mountain-name{
    font-weight: bold;
    cursor: pointer;
    color: black;
    text-decoration-color: cornflowerblue;
}
</style>