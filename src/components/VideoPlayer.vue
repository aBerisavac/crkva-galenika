<template>
    <div class="w-full px-4">
        <div
            class="relative overflow-hidden border border-[#756737]/60 bg-[#312905] shadow-[0_3px_10px_rgba(49,41,5,0.18)]">
            <video class="block w-full h-auto" :src="src" :poster="poster" controls playsinline preload="metadata">
                Ваш прегледач не подржава видео.
            </video>
        </div>

        <div v-if="title" class="flex items-center justify-center gap-3 mt-3 text-[#312905]">
            <div class="h-px flex-1 bg-[#756737]/40"></div>


            <p class="min-w-0 max-w-[75%] text-[15px] font-bold text-center whitespace-normal break-words leading-5">
                {{ title }}
            </p>


            <div class="h-px flex-1 bg-[#756737]/40"></div>
        </div>
    </div>
</template>

<script setup lang="ts">
defineProps({
    src: {
        type: String,
        required: true,
    },
    poster: {
        type: String,
        default: undefined,
    },
    title: {
        type: String,
        default: "",
    },
})
</script>

<style scoped></style>