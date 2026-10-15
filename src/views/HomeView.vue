<template>
    <div class="mt-0">
        <div class="flex flex-col sm:hidden">
            <img src="/assets/hero.png" />
            <p class="text-xs mr-2 mt-1 self-end">Нова Галеника</p>
        </div>


        <div class="hidden sm:block pt-24 pb-10 px-4">
            <div class="max-w-6xl mx-auto grid grid-cols-2 gap-12 items-center">
                <div class="flex flex-col items-start pl-4 lg:pl-10">
                    <div class="flex items-center gap-3 mb-5">
                        <span class="text-[#a47b32] text-2xl leading-none">☦</span>

                        <p class="text-sm font-semibold tracking-[0.15em] text-[#8b2f24] uppercase">
                            Српска православна црква
                        </p>
                    </div>

                    <h1 class="font-bold text-4xl xl:text-5xl leading-tight -tracking-tight text-[#211804]">
                        Храм Св. мученица Вере, Наде, Љубави и мајке им Софије
                    </h1>

                    <div class="flex items-center gap-3 w-full my-7">
                        <div class="h-px flex-1 bg-[#a47b32]/60"></div>
                        <span class="w-[8px] h-[8px] shrink-0 rotate-45 bg-[#8b2f24] border border-[#a47b32]"></span>
                        <div class="h-px flex-1 bg-[#a47b32]/60"></div>
                    </div>

                    <p class="text-lg tracking-wide text-[#756737]">
                        Нова Галеника
                    </p>
                </div>

                <div class="relative flex justify-center items-center">

                    <img src="/assets/hero-framed.png" class="w-full h-auto max-h-[460px] object-contain"
                        alt="Храм Св. мученица Вере, Наде, Љубави и мајке им Софије" />
                </div>
            </div>
        </div>


        <BannerComponent class="my-2 hidden sm:block" />

        <div class="flex items-center">
            <div class="p-4 lg:max-w-7xl lg:mx-auto  sm:w-[40%]">
                <div class="flex flex-col">
                    <p class="font-semibold text-lg leading-5.5 -tracking-tight">
                        Мала Госпојина рођење Пресвете Богородице, 21.09.2026. (понедељак). Бденије уочи празника у
                        18:00.
                        Литургија у 8:00. wfqwfqwf fqwfqwffqwf
                    </p>
                    <p class="text-sm text-amber-800 mt-1 self-end">September 19, 2026</p>
                </div>
                <div class="my-4">
                    <hr />
                </div>
                <div class="flex flex-col">
                    <p class="font-semibold text-lg leading-5.5 -tracking-tight">
                        Мала Госпојина рођење Пресвете Богородице, 21.09.2026. (понедељак). Бденије уочи празника у
                        18:00.
                        Литургија у 8:00. wfqwfqwf fqwfqwffqwf
                    </p>
                    <p class="text-sm text-amber-800 mt-1 self-end">September 19, 2026</p>
                </div>
                <div class="my-4">
                    <hr />
                </div>
                <div class="flex flex-col">
                    <p class="font-semibold text-lg leading-5.5 -tracking-tight">
                        Мала Госпојина рођење Пресвете Богородице, 21.09.2026. (понедељак). Бденије уочи празника у
                        18:00.
                        Литургија у 8:00. wfqwfqwf fqwfqwffqwf
                    </p>
                    <p class="text-sm text-amber-800 mt-1 self-end">September 19, 2026</p>
                </div>

                <PaginationToolbar class="mt-4" v-model="pageable" />
            </div>

            <div class="p-4 lg:max-w-7xl lg:mx-auto hidden sm:block">
                <img src="/assets/Vreme_Liturgije.png" class=" h-[50vh] m-auto" />
            </div>
        </div>

        <BannerComponent class="my-2 sm:hidden" />

        <div class="p-4 lg:max-w-7xl lg:mx-auto sm:hidden">
            <img src="/assets/Vreme_Liturgije.png" class=" h-[50vh] m-auto" />
        </div>

        <ContactInfo />
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import PaginationToolbar from '../components/pagination/PaginationToolbar.vue';
import type { IPageable } from '../models/interfaces/IPageable.ts';
import BannerComponent from '../components/decoration/BannerComponent.vue';
import ContactInfo from '../components/ContactInfo.vue';

const pageable = ref<IPageable>({
    page: 1,
    pages: 12,
    pageSize: 24,
    totalItems: 288
})

</script>

<style scoped></style>
