<script setup lang="ts">
    import { ref } from "@vue/reactivity";
    import cardoffre from "./card.vue";

    // On fait une variable réactive qui réactive qui réference les données
    // ATTENTION : faire une Ref pas une Reactive car :
    // c'est l'objet qui doit être réactif, pas ses props
    const maison = ref({nom:"test-ref-formkit", price:29, favoris:false, txt:"test de formkit", nbbath:4, nblit:3, nbsize:"89 m²", img:"/card.jpg"});
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
            <FormKit type="form" v-model="maison"
            :config="{
                        classes: {
                                    input: 'p-1 rounded border-gray-300 shadow-sm border bg-red-300 hover:bg-green-500 hover:border-4 hover:animate-pulse',
                                    label: 'text-gray-600',
                                },
                    }"
            :submit-attrs="{ classes: { input: 'bg-green-300 px-6 py-2 rounded-full text-center' } }">
                <FormKit name="nom" label="nom"/>
                <FormKit name="txt" label="Desicription"/>
                <FormKit name="price" label="prix" type="number"/>
                <div class="flex gap-5">
                    <FormKit name="nbsize" label="Superficie"/>
                    <FormKit name="nblit" label="Nombre de lit" type="number"/>
                    <FormKit name="nbbath" label="Nombre de Salle de bains" type="number"/>
                </div>
                <FormKit name="favoris" label="mettre en valeur" type="checkbox" wrapper-class="flex gap-4"/>
            </FormKit>
        </div>
    </div>
</template>