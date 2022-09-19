<template>
<div class="p-2">
    <h1 class="text-2xl">Page Simple</h1>
    <card class="w-1/2" v-bind="objet"/>
</div>
</template>

<script setup lang="ts">
    import card from "../components/card.vue";

    const objet = {nom:"test", price:34, favoris:true, txt:"produit de test", nbbath:2, nbsize:"test m²", img:"/public/card.jpg"}
</script>