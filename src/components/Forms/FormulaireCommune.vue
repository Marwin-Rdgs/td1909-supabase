<script setup lang="ts">
    import { ref } from "@vue/reactivity";
    import { supabase } from "../../supabase.ts";
    import cardoffre from "../card.vue";

    import { useRouter } from "vue-router";
    const router = useRouter();

  const props = defineProps(["id"]);
if (props.id) {
    // On charge les données de la maison
    let { data: Commune, error } = await supabase
        .from("Commune")
        .select("*")
        .eq("id_Commune", props.id);
    if (error) console.log("n'a pas pu charger le table Commune :", error);
    else Commune.value = (data as any[])[0];
}

    // On fait une variable réactive qui réactive qui réference les données
    // ATTENTION : faire une Ref pas une Reactive car :
    // c'est l'objet qui doit être réactif, pas ses props
    // const maison = ref({nomMaison:"test-ref-formkit", prixMaison:29, favoris:false, adressMaison:"test de formkit", nbrBath:4, nbrChambres:3, surfaceMaison:"89 m²", imgMaison:"/card.jpg"});

    async function upsertCommune(dataForm, node) {
    const { data, error } = await supabase.from("Commune").upsert(dataForm);
    if (error || !data) node.setErrors([error?.message])
    else {
    node.setErrors([]);
    router.push({ name: "edit-id", params: { id_Commune: data[0].id} });
    }
}

</script>

<template>
    <div>
        <div class="p-2">
                <h2> Liste des communes</h2>
            <ul>
                <li v-for="Commune in Commune" :key="Commune.libelle_Commune">
                    <p>{{ Commune.libelle_Commune }}</p>
                </li>
            </ul>

            <!-- On passe la "ref" à Formkit -->
            <FormKit type="form" v-model="Commune" @submit="upsertCommune"
            :config="{
                        classes: {
                                    input: 'p-1 rounded border-gray-300 shadow-sm border bg-red-300 hover:bg-green-500 hover:border-4 hover:animate-pulse',
                                    label: 'text-gray-600',
                                },
                    }"
            :submit-attrs="{ classes: { input: 'bg-green-300 px-6 py-2 rounded-full text-center' } }">
                <FormKit name="libelle_Commune" label="nom"/>
                <!-- <FormKit name="favoris" label="mettre en valeur" type="checkbox" wrapper-class="flex gap-4"/> -->
            </FormKit>
        </div>
    </div>
</template>