<template>
    <footer class="w-full px-4 py-5 text-center text-[#312905]/70">
        <div class="flex items-center justify-center gap-3 mb-2">
            <div class="h-px w-full bg-[#756737]/40"></div>
        </div>

        <div class="p-4 w-full sm:w-1/2 m-auto">
            <VideoPlayer
                src="https://crkva-galenika.rs/wp-content/uploads/2024/02/Тропар-Светих-мученица-Вере-Наде-Љубави-и-мајке-им-Софије-3.mp4"
                title="Тропар Светих мученица Вере, Наде, Љубави и мајке им Софије" />
        </div>

        <div class="p-4 w-full sm:w-1/2 m-auto">
            <VideoPlayer
                src="https://crkva-galenika.rs/wp-content/uploads/2024/02/Кондак-Светих-мученица-Вере-Наде-Љубави-и-мајке-им-Софије.mp4"
                title="Кондак Светих мученица Вере, Наде, Љубави и мајке им Софије" />
        </div>

        <div class="flex items-center justify-center gap-3 mb-2">
            <div class="h-px w-full bg-[#756737]/40"></div>
        </div>

        <p class="text-[13px] italic tracking-[0.02em]">
            Са пажњом израдио Берисавац Алекса
        </p>
    </footer>
</template>

<script setup lang="ts">
import VideoPlayer from '../VideoPlayer.vue';


</script>

<style scoped></style>