<template>
    <div class="p-2">
        <h1 class="text-2xl">Page Liste Supabase</h1>
        <div v-for="Maisons in Maisons" :key="Maisons.nomMaison">
            <card class="w-1/2" v-bind="Maisons"/>
        </div>
    </div>
    </template>

<script setup lang="ts">
    import card from "../components/card.vue";
    import { supabase } from "../supabase.ts";

    console.log("supabase :", supabase); // pour vérifier et "garder" supabase dans le code
    // const Maisons = []; ------> à remplacer par l'appel à Supabase

    let { data: Maisons, error } = await supabase
  .from('Maisons')
  .select('*')

</script>