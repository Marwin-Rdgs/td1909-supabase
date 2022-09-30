<script setup lang="ts">
    import { ref } from "@vue/reactivity";
    import { supabase } from "../supabase.ts";
    import cardoffre from "./card.vue";

    let { data: Maisons, error } = await supabase
  .from('Maisons')
  .select('*')

    // On fait une variable réactive qui réactive qui réference les données
    // ATTENTION : faire une Ref pas une Reactive car :
    // c'est l'objet qui doit être réactif, pas ses props
    // const maison = ref({nomMaison:"test-ref-formkit", prixMaison:29, favoris:false, adressMaison:"test de formkit", nbrBath:4, nbrChambres:3, surfaceMaison:"89 m²", imgMaison:"/card.jpg"});

    async function upsertMaison(dataForm, node) {
    const { data, error } = await supabase.from("Maisons").upsert(dataForm);
    if (error) node.setErrors([error.message])
}

</script>

<template>
    <div>
        <div class="p-2">
            <h2 class="text-2xl">Résultat (Prévisualisation)</h2>
            <!-- Optionnel on affiche les données -->
            <cardoffre v-bind="maison" />

        </div>
        <div class="p-2">
            <!-- On passe la "ref" à Formkit -->
            <FormKit type="form" v-model="Maisons" @submit="upsertMaison"
            :config="{
                        classes: {
                                    input: 'p-1 rounded border-gray-300 shadow-sm border bg-red-300 hover:bg-green-500 hover:border-4 hover:animate-pulse',
                                    label: 'text-gray-600',
                                },
                    }"
            :submit-attrs="{ classes: { input: 'bg-green-300 px-6 py-2 rounded-full text-center' } }">
                <FormKit name="nomMaison" label="nom"/>
                <FormKit name="adressMaison" label="Desicription"/>
                <FormKit name="prixMaison" label="prix" type="number"/>
                <FormKit name="imgMaison" label="URL de l'image"/>
                <div class="flex gap-5">
                    <FormKit name="surfaceMaison" label="Superficie"/>
                    <FormKit name="nbrChambres" label="Nombre de lit" type="number"/>
                    <FormKit name="nbrBath" label="Nombre de Salle de bains" type="number"/>
                </div>
                <!-- <FormKit name="favoris" label="mettre en valeur" type="checkbox" wrapper-class="flex gap-4"/> -->
            </FormKit>
        </div>
    </div>
</template>