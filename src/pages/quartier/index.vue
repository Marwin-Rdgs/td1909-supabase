<script setup lang="ts">
    import { supabase } from "../../supabase.ts";
    const { data, error } = await supabase.from("Quartier").select("*");
    if (error) console.log("n'a pas pu charger la table quartier :", error);

    import { useRouter } from "vue-router";
</script>
    
    <template>
      <section class="flex flex-col">
        <h3 class="text-2xl">Liste des quartiers</h3>
        <ul>
          <li v-for="quartierObject in (data as any[])">
            {{ quartierObject.libelle_Commune }} -
            {{ quartierObject.libelle_Quartier }}
          </li>
        </ul>
      </section>
    </template>