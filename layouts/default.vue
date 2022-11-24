<template>
    <div>

        <div class="navbar">
            <NuxtLink to="/" >home</NuxtLink>
            <NuxtLink to="/about" >about</NuxtLink>
            <NuxtLink to="/about/stan" >person</NuxtLink>
            <NuxtLink to="/about/434" >age</NuxtLink>
        </div>
        <div>
            <slot></slot>
        </div>
    </div>
</template>

<script setup>

import { ref } from 'vue'

const name = ref('wanja')

</script>

<style scoped>

</style>