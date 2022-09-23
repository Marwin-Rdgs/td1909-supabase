<template>
    <div class="p-2">
        <h1 class="text-2xl">Page Liste</h1>
        <div v-for="maisons in maisons" :key="maisons.nom">
            <card class="w-1/2" v-bind="maisons"/>
        </div>
    </div>
    </template>

<script setup lang="ts">
    import card from "../components/card.vue";

  const maisons = [{nomMaison:"test", prixMaison:34, favoris:true, adressMaison:"produit de test", nbrBath:2, surfaceMaison:"test m²", imgMaison:"/public/card.jpg"}, {nomMaison:"test2", prixMaison:27, favoris:false, adressMaison:"2ème produit de test", nbrBath:2, surfaceMaison:"test*2 m²", imgMaison:"/public/card.jpg"}, {nomMaison:"Dernier test", prixMaison:86, adressMaison:"Dernier produit de test", nbrBath:1, surfaceMaison:"test m²", imgMaison:"/public/card.jpg"}]
//   import maisons from "../assets/maisons.json";
</script>