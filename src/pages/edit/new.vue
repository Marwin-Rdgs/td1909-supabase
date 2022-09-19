<script setup>
    import cardoffre from "../../components/card.vue";
    import offremaison from "../../components/FormulaireOffreMaison.vue"

    const maisonex = {nom:"test", price:34, favoris:false, txt:"produit de test", nbbath:2, nbsize:"test m²", img:"/card.jpg"};
</script>

<template>
    <div class="p-2">
        <h1 class="text-2xl">Page New</h1>

        <cardoffre class="w-1/3" v-bind="maisonex"/>

        <offremaison class="w-1/2"/>
    </div>
    </template>