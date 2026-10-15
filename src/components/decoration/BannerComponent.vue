<template> 
    <div class="relative w-full h-8 overflow-hidden bg-[#3f472c] border-y border-[#756737]/60 shadow-[inset_0_1px_0_rgba(255,238,190,0.1),inset_0_-1px_0_rgba(20,18,8,0.25)]"> 
        <span class="sr-only"> 
            {{ bannerText }} 
        </span> 
 
        <div class="marquee-track absolute inset-y-0 left-0 flex w-max items-center"> 
            <div class="marquee-group flex shrink-0 items-center" aria-hidden="true"> 
                <template v-for="index in 3" :key="`first-${index}`"> 
                    <span class="whitespace-nowrap text-[16px] leading-none font-bold tracking-[0.025em] text-[#f1e3bd]"> 
                        {{ bannerText }} 
                    </span> 
 
                    <span class="mx-5 w-[6px] h-[6px] shrink-0 rotate-45 bg-[#8b2f24] border border-[#b85a43]/70"></span> 
                </template> 
            </div> 
 
            <div class="marquee-group flex shrink-0 items-center" aria-hidden="true"> 
                <template v-for="index in 3" :key="`second-${index}`"> 
                    <span class="whitespace-nowrap text-[16px] leading-none font-bold tracking-[0.025em] text-[#f1e3bd]"> 
                        {{ bannerText }} 
                    </span> 
 
                    <span class="mx-5 w-[6px] h-[6px] shrink-0 rotate-45 bg-[#8b2f24] border border-[#b85a43]/70"></span> 
                </template> 
            </div> 
        </div> 
    </div> 
</template> 
 
<script setup lang="ts"> 
const bannerText = "Храм Св. мученица Вере, Наде, Љубави и мајке им Софије - Нова Галеника" 
</script> 
 
<style scoped> 
.marquee-track { 
    animation: marquee 64s linear infinite; 
    will-change: transform; 
} 
 
@keyframes marquee { 
    from { 
        transform: translateX(0); 
    } 
 
    to { 
        transform: translateX(-50%); 
    } 
} 
 
@media (prefers-reduced-motion: reduce) { 
    .marquee-track { 
        animation-play-state: paused; 
    } 
} 
</style>