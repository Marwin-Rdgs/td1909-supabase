<script setup>
    import cardoffre from "../../components/card.vue";
    import offremaison from "../../components/FormulaireOffreMaison.vue"

    const maisonex = {nomMaison:"test", prixMaison:34, favoris:false, adressMaison:"produit de test", nbrBath:2, surfaceMaison:"test m²", imgMaison:"/card.jpg"};
</script>

<template>
    <div class="p-2">
        <h1 class="text-2xl">Page New</h1>

        <cardoffre class="w-1/3" v-bind="maisonex"/>

        <offremaison class="w-1/2"/>
    </div>
    </template>