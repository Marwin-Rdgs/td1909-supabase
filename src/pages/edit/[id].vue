<script setup lang="ts">
    import cardoffre from "../../components/card.vue";
    import offremaison from "../../components/Forms/FormulaireOffreMaison.vue"
    import { supabase } from "@/supabase"

defineProps({
        id_maison : String,
        id_Quartier : String,
        id_Commune : String,
        id_agent : String,
    })

</script>

<template>
    
    <div class="p-2">
        <h1 class="text-2xl">Page Edit-new</h1>

        <!-- <cardoffre class="w-1/3" v-model="Maisons"/> -->

        <offremaison class="w-1/2" :id_maison="id_maison"/>
    </div>

</template>