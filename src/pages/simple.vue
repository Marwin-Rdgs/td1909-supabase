<template>
<div class="p-2">
    <h1 class="text-2xl">Page Simple</h1>
    <card class="w-1/2" v-bind="objet"/>
</div>
</template>

<script setup lang="ts">
    import card from "../components/card.vue";

    const objet = {nomMaison:"test", prixMaison:34, favoris:true, adressMaison:"produit de test", nbrBath:2, surfaceMaison:"test m²", imgMaison:"/public/card.jpg"}
</script>