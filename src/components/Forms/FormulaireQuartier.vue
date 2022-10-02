<script setup lang="ts">
    import { ref } from "@vue/reactivity";
    import { supabase } from "../../supabase.ts";
    import cardoffre from "../card.vue";

    import { useRouter } from "vue-router";
    const router = useRouter();

  const props = defineProps(["id"]);
if (props.id) {
    // On charge les données de la maison
    let { data: Quartier, error } = await supabase
        .from("Quartier")
        .select("*")
        .eq("id_Quartier", props.id);
    if (error) console.log("n'a pas pu charger le table Commune :", error);
    else Quartier.value = (data as any[])[0];
}

    // On fait une variable réactive qui réactive qui réference les données
    // ATTENTION : faire une Ref pas une Reactive car :
    // c'est l'objet qui doit être réactif, pas ses props
    // const maison = ref({nomMaison:"test-ref-formkit", prixMaison:29, favoris:false, adressMaison:"test de formkit", nbrBath:4, nbrChambres:3, surfaceMaison:"89 m²", imgMaison:"/card.jpg"});

    async function upsertQuartier(dataForm, node) {
    const { data, error } = await supabase.from("Quartier").upsert(dataForm);
    if (error || !data) node.setErrors([error?.message])
    else {
    node.setErrors([]);
    router.push({ name: "edit-id", params: { id_Quartier: data[0].id} });
    }
}

</script>

<template>
    <div>
        <div class="p-2">
                <h2> Liste des Quartiers</h2>
            <ul>
                <li v-for="Quartier in Quartier" :key="Quartier.libelle_quartier">
                    <p>{{ Quartier.libelle_Quartier }}</p>
                </li>
            </ul>

            <!-- On passe la "ref" à Formkit -->
            <FormKit type="form" v-model="Quartier" @submit="upsertQuartier"
            :config="{
                        classes: {
                                    input: 'p-1 rounded border-gray-300 shadow-sm border bg-red-300 hover:bg-green-500 hover:border-4 hover:animate-pulse',
                                    label: 'text-gray-600',
                                },
                    }"
            :submit-attrs="{ classes: { input: 'bg-green-300 px-6 py-2 rounded-full text-center' } }">
                <FormKit name="libelle_quartier" label="nom"/>
            </FormKit>
        </div>
    </div>
</template>