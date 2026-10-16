<template>
    <nav class="top-0 w-full z-[100] transition-[background-color,box-shadow] duration-300 sm:!fixed sm:!bg-[#713c31] sm:!shadow-none sm:border-b sm:border-[#a47b32]/35"
        :class="isScrolled
            ? 'fixed bg-[#713c31] shadow-[0_3px_12px_rgba(49,24,12,0.28)]'
            : 'absolute'">


        <div class="relative w-full flex sm:hidden">
            <div v-if="!isScrolled" class="absolute flex w-full justify-end overflow-hidden">
                <img src="/assets/nav-triangle-cutout-ver1.png" class="w-[180px] -mt-2 -mr-2" />
            </div>

            <div class="w-full flex items-center justify-between transition-[padding] duration-300"
                :class="isScrolled ? 'px-4 py-2' : 'p-4'">
                <div class="flex gap-3 items-center min-w-0">
                    <div v-if="isScrolled"
                        class="shrink-0 w-10 h-10 flex items-center justify-center rounded-lg bg-[#f1e3bd] border border-[#000000]/90 p-px shadow-[0_1px_3px_rgba(33,24,4,0.2)]">
                        <img src="/assets/Coat_of_arms_of_Serbian_Orthodox_Church.png"
                            class="w-full h-full object-contain filter-[sepia(0.65)]"
                            alt="Грб Српске православне цркве" />
                    </div>

                    <div v-else class="shrink-0 w-14 h-14 flex items-center justify-center">
                        <img src="/assets/Coat_of_arms_of_Serbian_Orthodox_Church.png"
                            class="w-full h-full object-contain filter-[sepia(0.65)]"
                            alt="Грб Српске православне цркве" />
                    </div>

                    <div class="relative min-w-0">
                        <div v-if="!isScrolled"
                            class="absolute -inset-x-4 -inset-y-2 bg-[radial-gradient(ellipse_at_center,rgba(244,201,82,0.80)_0%,rgba(225,169,54,0.35)_55%,rgba(225,169,54,0)_100%)] blur-[3px]">
                        </div>

                        <h1 class="relative font-bold flex flex-col -tracking-tight transition-[font-size,line-height,color] duration-300"
                            :class="isScrolled
                                ? 'text-[14px] leading-4 text-[#f1e3bd]'
                                : 'text-xl leading-5.5 text-[#211804] [text-shadow:0_1px_1px_rgba(255,220,120,0.55)]'">
                            <span>
                                Храм Св. мученица
                            </span>
                            <span>
                                Вере, Наде, Љубави
                            </span>
                            <span>
                                и мајке им Софије
                            </span>
                        </h1>
                    </div>
                </div>

                <button type="button"
                    class="relative z-1 shrink-0 w-10 h-10 flex items-center justify-center transition-[color,margin] duration-300"
                    :class="isScrolled
                        ? 'text-[#f1e3bd]'
                        : 'text-[#211804] -mt-10'" :aria-expanded="isMenuOpen" aria-label="Отвори мени"
                    @click="openMenu">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32" fill="none" stroke="currentColor"
                        stroke-width="2.8" stroke-linecap="round" class="w-8 h-8">
                        <path d="M6 9h20" />
                        <path d="M6 16h20" />
                        <path d="M6 23h20" />
                    </svg>
                </button>
            </div>
        </div>

        <div class="hidden sm:flex w-full items-center justify-between px-4 py-2">
            <RouterLink to="/" class="flex items-center shrink-0">
                <div
                    class="w-10 h-10 shrink-0 flex items-center justify-center rounded-lg bg-[#f1e3bd] border border-[#000000]/50 p-px shadow-[0_1px_3px_rgba(33,24,4,0.2)]">
                    <img src="/assets/Coat_of_arms_of_Serbian_Orthodox_Church.png"
                        class="w-full h-full object-contain filter-[sepia(0.65)]" alt="Грб Српске православне цркве" />
                </div>
            </RouterLink>


            <div class="flex items-center gap-8">
                <RouterLink v-for="item in menuItems" :key="item.to" :to="item.to"
                    class="text-[#f1e3bd] font-medium text-[15px] tracking-wide transition-colors duration-200 hover:text-[#e3bc75]"
                    active-class="!text-[#e3bc75]">
                    {{ item.label }}
                </RouterLink>
            </div>

        </div>
    </nav>

    <Transition name="backdrop">
        <div v-if="isMenuOpen" class="fixed inset-0 z-[110] bg-[#211804]/45 sm:hidden" @click="closeMenu">
        </div>
    </Transition>

    <Transition name="drawer">
        <aside v-if="isMenuOpen"
            class="fixed top-0 right-0 z-[120] h-dvh w-[82%] max-w-[320px] bg-[#f1e3bd] border-l border-[#756737]/60 shadow-[-8px_0_24px_rgba(49,24,12,0.25)] sm:hidden">
            <div class="h-full flex flex-col">
                <div class="h-16 px-4 flex items-center justify-between bg-[#3f472c] border-b border-[#756737]/60">
                    <div class="flex items-center gap-3">
                        <span class="w-[9px] h-[9px] shrink-0 rotate-45 bg-[#713c31] border border-[#b85a43]/70"></span>

                        <span class="text-[18px] font-bold tracking-[0.08em] text-[#f1e3bd]">
                            Мени
                        </span>
                    </div>

                    <button type="button" class="w-9 h-9 flex items-center justify-center text-[#f1e3bd]"
                        aria-label="Затвори мени" @click="closeMenu">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            stroke-width="2" stroke-linecap="round" class="w-6 h-6">
                            <path d="M6 6l12 12" />
                            <path d="M18 6L6 18" />
                        </svg>
                    </button>
                </div>

                <div class="flex-1 px-4 py-4">
                    <nav class="flex flex-col">
                        <RouterLink v-for="(item, index) in menuItems" :key="item.to" :to="item.to"
                            class="group flex items-center gap-3 py-4 px-2 border-b border-[#756737]/30 text-[#312905] font-bold text-[17px] transition-all duration-200 hover:pl-3 hover:text-[#713c31]"
                            @click="closeMenu">
                            <span>
                                {{ item.label }}
                            </span>

                            <span
                                class="ml-auto flex items-center gap-2 text-[#713c31]/55 text-sm transition-colors duration-200 group-hover:text-[#713c31]">
                                {{ String(index + 1).padStart(2, "0") }}

                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none"
                                    stroke="currentColor" stroke-width="1.8" stroke-linecap="round"
                                    stroke-linejoin="round"
                                    class="w-4 h-4 transition-transform duration-200 group-hover:translate-x-1">
                                    <path d="m9 18 6-6-6-6" />
                                </svg>
                            </span>
                        </RouterLink>
                    </nav>
                </div>

                <div class="px-4 py-5 text-center">
                    <div class="flex items-center justify-center gap-3 mb-2">
                        <div class="h-px w-8 bg-[#756737]/40"></div>

                        <span class="w-[5px] h-[5px] rotate-45 bg-[#713c31]/70"></span>

                        <div class="h-px w-8 bg-[#756737]/40"></div>
                    </div>

                    <p class="text-[12px] italic text-[#312905]/60">
                        Нова Галеника
                    </p>
                </div>
            </div>
        </aside>
    </Transition>
</template>

<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref, watch } from "vue"

type MenuItem = {
    label: string
    to: string
}

const isScrolled = ref(false)
const isMenuOpen = ref(false)

const menuItems: MenuItem[] = [
    {
        label: "Опција 1",
        to: "/option-1",
    },
    {
        label: "Опција 2",
        to: "/option-2",
    },
]

let ticking = false
let previousHtmlOverflow = ""
let isScrollLocked = false

const updateScrollState = () => {
    if (!isMenuOpen.value) {
        isScrolled.value = window.scrollY > 0
    }

    ticking = false
}

const handleScroll = () => {
    if (ticking) {
        return
    }

    ticking = true

    requestAnimationFrame(updateScrollState)
}

const openMenu = () => {
    isMenuOpen.value = true
}

const closeMenu = () => {
    isMenuOpen.value = false
}

const handleKeydown = (event: KeyboardEvent) => {
    if (event.key === "Escape") {
        closeMenu()
    }
}

const handleResize = () => {
    if (window.innerWidth >= 640 && isMenuOpen.value) {
        closeMenu()
    }
}

const unlockScroll = () => {
    if (!isScrollLocked) {
        return
    }

    document.documentElement.style.overflow = previousHtmlOverflow
    isScrollLocked = false
}

watch(isMenuOpen, (isOpen) => {
    if (isOpen) {
        if (!isScrollLocked) {
            previousHtmlOverflow = document.documentElement.style.overflow
            document.documentElement.style.overflow = "hidden"
            isScrollLocked = true
        }

        return
    }

    unlockScroll()
    updateScrollState()
})

onMounted(() => {
    updateScrollState()

    window.addEventListener("scroll", handleScroll, { passive: true })
    window.addEventListener("keydown", handleKeydown)
    window.addEventListener("resize", handleResize)
})

onBeforeUnmount(() => {
    window.removeEventListener("scroll", handleScroll)
    window.removeEventListener("keydown", handleKeydown)
    window.removeEventListener("resize", handleResize)

    unlockScroll()
})
</script>

<style scoped>
.drawer-enter-active,
.drawer-leave-active {
    transition: transform 300ms ease;
}

.drawer-enter-from,
.drawer-leave-to {
    transform: translateX(100%);
}

.drawer-enter-to,
.drawer-leave-from {
    transform: translateX(0);
}

.backdrop-enter-active,
.backdrop-leave-active {
    transition: opacity 250ms ease;
}

.backdrop-enter-from,
.backdrop-leave-to {
    opacity: 0;
}

.backdrop-enter-to,
.backdrop-leave-from {
    opacity: 1;
}
</style>
