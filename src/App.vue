<script setup lang="ts">
import FooterComponent from './components/navigation/FooterComponent.vue';
import NavBar from './components/navigation/NavBar.vue';

</script>

<template>
    <div class="min-h-screen flex flex-col relative">

      <NavBar />
      <main class="">
        <RouterView></RouterView>
      </main>
      <FooterComponent />

    </div>
</template>