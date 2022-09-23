<template>
    <div class="p-2">
        <h1 class="text-2xl">Page Liste Fetch</h1>
        <div v-for="maisons in maisons" :key="maisons.nomMaison">
            <card class="w-1/2" v-bind="maisons"/>
        </div>
    </div>
    </template>

<script setup lang="ts">
    import card from "../components/card.vue";

    const res = await fetch("maisons.json");
    const maisons = await res.json();

</script>