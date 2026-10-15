
<template>
    <div class="w-full px-4">
        <div
            class="relative overflow-hidden border border-[#756737]/60 bg-[#312905] shadow-[0_3px_10px_rgba(49,41,5,0.18)]">
            <button v-if="!isVideoLoaded" type="button"
                class="group relative block w-full cursor-pointer"
                aria-label="Пусти видео" @click="loadVideo">
                <img src="/assets/sv-mucenice.png"
                    class="block w-full h-auto"
                    alt="Свете мученице Вера, Нада, Љубав и мајка Софија" />

                <div class="absolute inset-0 bg-[#211804]/20 transition-colors duration-300 group-hover:bg-[#211804]/30">
                </div>

                <div
                    class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-16 h-16 sm:w-20 sm:h-20 rounded-full flex items-center justify-center bg-[#713c31]/90 border border-[#e3bc75]/70 shadow-[0_4px_16px_rgba(33,24,4,0.4)] transition-transform duration-300 group-hover:scale-110">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
                        fill="currentColor" class="w-8 h-8 sm:w-10 sm:h-10 text-[#f1e3bd] ml-1">
                        <path d="M8 5v14l11-7z" />
                    </svg>
                </div>
            </button>

            <video v-else ref="videoRef" class="block w-full h-auto" :src="src" :poster="poster"
                controls playsinline preload="metadata">
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
import { nextTick, ref } from "vue"

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

const isVideoLoaded = ref(false)
const videoRef = ref<HTMLVideoElement | null>(null)

const loadVideo = async () => {
    isVideoLoaded.value = true

    await nextTick()

    try {
        await videoRef.value?.play()
    } catch (error) {
        console.error("Video autoplay failed:", error)
    }
}
</script>

<style scoped></style>
