<script setup lang="ts">
    import groupBy from "lodash/groupBy"
    import { supabase } from "../../supabase";
    const { data, error } = await supabase.from("quartiercommune").select("*");
    if (error) console.log("n'a pas pu charger la table quartiercommune :", error);
    </script>
    
    <template>
      <section class="flex flex-col">
        <h3 class="text-2xl">Liste des quartiers</h3>
        <!-- <DisclosurePanel> -->
        <ul>
          <li v-for="quartierObject in (data as any[])">
            {{ quartierObject.libelle_Commune }} -
            {{ quartierObject.libelle_quartier }}
          </li>
        </ul>
    <!-- </DisclosurePanel> -->

        <!-- <Disclosure v-for="(Quartier, libelle_Commune) in groupBy(data, 'libelle_Commune')" :key="libelle_Commune" />
        <DisclosureButton> {{ Quartier.libelle_Commune }}</DisclosureButton> -->

      </section>
    </template>