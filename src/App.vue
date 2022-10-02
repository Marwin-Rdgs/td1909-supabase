<template>
  <nav>
    <h4 class="text-xl">
      <Bars3Icon class="inline-block h-5 w-5 text-blue-500" />
      menu (dans <code class="font-mono">/src/App.vue</code>)
    </h4>
    <ul class="border-4">
      <li class="mb-4">
        <router-link class="text-red-600 underline" to="/">
          lien vers
          <code class="font-mono">/src/pages/index.vue</code>
        </router-link>
      </li>
      <li class="mb-4">
        <router-link class="text-red-600 underline" to="/simple">
          <h2>lien vers Page Simple</h2>
        </router-link>
      </li>
   <li class="mb-4">
        <h1>Liens vers les différentes listes</h1>
        <div class="flex gap-4">
          <router-link class="text-red-600 underline" to="/liste"><h2>lien vers Page Liste</h2></router-link>
          <router-link class="text-red-600 underline" to="/liste-fetch"><h2>lien vers Page Liste-fetch</h2></router-link>
          <router-link class="text-red-600 underline" to="/liste-supabase"><h2>lien vers Page Liste-supabase</h2></router-link>
      </div>
  </li>

  <li class="mb-4">
        <h1>Liens vers les différentes "New"</h1>
    <div class="flex gap-4">
        <router-link class="text-red-600 underline" to="/new/newMaison"><h2>New Maison</h2></router-link>
        <router-link class="text-red-600 underline" to="/new/newCommune"><h2>New Commune</h2></router-link>
        <router-link class="text-red-600 underline" to="/new/newQuartier"><h2>New Quartier</h2></router-link>
        <router-link class="text-red-600 underline" to="/new/newAgent"><h2>New Agent</h2></router-link>
    </div>
  </li>

  <li class="mb-4">
        <h1>TP 4 - Liste Simple</h1>
    <div class="flex gap-4">
        <router-link class="text-red-600 underline" to="/quartier/index"><h2>Quartier</h2></router-link>
    </div>
  </li>


      <li class="mb-4">
        <h1>Login / Logout</h1>
        <router-link class="text-red-600 underline" to="/login">
          <h2>Cliquez ici</h2>
        </router-link>
      </li>

    </ul>
  </nav>

  <!-- Affiche les pages -->
 <Suspense> <router-view class="m-2 border-2 p-2" /></Suspense>
</template>


<script setup lang="ts">
import { Bars3Icon } from '@heroicons/vue/20/solid'
</script>
