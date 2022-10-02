<script setup lang="ts">
    import { ref } from "@vue/reactivity";
    import { supabase } from "../../supabase.ts";
    import cardoffre from "../card.vue";

    import { useRouter } from "vue-router";

  const props = defineProps(["id"]);
if (props.id) {
    // On charge les données de la maison
    let { data: Agent, error } = await supabase
        .from("Agent")
        .select("*")
        .eq("id_agent", props.id);
    if (error) console.log("n'a pas pu charger le table Agent :", error);
    else Agent.value = (data as any[])[0];
}

    // On fait une variable réactive qui réactive qui réference les données
    // ATTENTION : faire une Ref pas une Reactive car :
    // c'est l'objet qui doit être réactif, pas ses props
    // const maison = ref({nomMaison:"test-ref-formkit", prixMaison:29, favoris:false, adressMaison:"test de formkit", nbrBath:4, nbrChambres:3, surfaceMaison:"89 m²", imgMaison:"/card.jpg"});

    async function upsertAgent(dataForm, node) {
    const { data, error } = await supabase.from("Agent").upsert(dataForm);
    if (error || !data) node.setErrors([error?.message])
    else {
    node.setErrors([]);
    router.push({ name: "edit-id", params: { id_Agent: data[0].id} });
    }
}

</script>

<template>
    <div>
        <div class="p-2">
                <h2> Liste des Agents</h2>
            <ul>
                <li v-for="Agent in Agent" :key="Agent.prenom_agent">
                    <p>{{ Agent.prenom_agent }} {{ Agent.nom_agent }} </p>
                </li>
            </ul>

            <!-- On passe la "ref" à Formkit -->
            <FormKit type="form" v-model="Agent" @submit="upsertAgent"
            :config="{
                        classes: {
                                    input: 'p-1 rounded border-gray-300 shadow-sm border bg-red-300 hover:bg-green-500 hover:border-4 hover:animate-pulse',
                                    label: 'text-gray-600',
                                },
                    }"
            :submit-attrs="{ classes: { input: 'bg-green-300 px-6 py-2 rounded-full text-center' } }">
            <div class="flex gap-2">
                <FormKit name="prenom_agent" label="prenom"/>
                <FormKit name="nom_agent" label="nom"/>
            </div>
            </FormKit>
        </div>
    </div>
</template>