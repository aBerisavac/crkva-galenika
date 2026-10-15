<template>
    <div class="w-full flex items-center justify-center">
        <div class="w-full flex items-center justify-between gap-3 text-[#312905]">
            <button type="button"
                class="shrink-0 w-9 h-9 flex items-center justify-center rounded-sm border border-[#6f5725]/45 bg-[#d6ab49]/10 text-2xl leading-none shadow-[inset_0_0_8px_rgba(92,65,15,0.08)] transition-all disabled:opacity-25 active:scale-95"
                :disabled="isFirstPage" aria-label="Претходна страница" @click="previousPage">
                ‹
            </button>

            <div class="min-w-0 flex items-center justify-center gap-1.5 whitespace-nowrap">

                <span class="text-sm opacity-65">
                    Страна
                </span>

                <input v-model="inputPage" type="number" :min="1" :max="model.pages" inputmode="numeric"
                    class="page-input w-9 h-7 px-1 flex items-center justify-center rounded-sm border border-[#72591f]/45 bg-[#d6ab49]/15 font-bold text-center outline-none focus:border-[#72591f]/80"
                    aria-label="Тренутна страница" @blur="commitPage" @keydown.enter.prevent="commitPage" />

                <span class="text-sm opacity-45">
                    /
                </span>

                <span class="text-sm">
                    {{ model.pages }}
                </span>
            </div>

            <button type="button"
                class="shrink-0 w-9 h-9 flex items-center justify-center rounded-sm border border-[#6f5725]/45 bg-[#d6ab49]/10 text-2xl leading-none shadow-[inset_0_0_8px_rgba(92,65,15,0.08)] transition-all disabled:opacity-25 active:scale-95"
                :disabled="isLastPage" aria-label="Следећа страница" @click="nextPage">
                ›
            </button>
        </div>
    </div>
</template>

<script setup lang="ts">
import { computed, ref, watch } from "vue"

type Pageable = {
    totalItems: number
    page: number
    pages: number
    pageSize?: number
}

const model = defineModel<Pageable>({ required: true })

const inputPage = ref<string | number>(model.value.page)

const isFirstPage = computed(() => model.value.page <= 1)

const isLastPage = computed(() => model.value.page >= model.value.pages)

watch(
    () => model.value.page,
    (page) => {
        inputPage.value = page
    }
)

const setPage = (page: number) => {
    const newPage = Math.min(Math.max(page, 1), Math.max(model.value.pages, 1))

    model.value = {
        ...model.value,
        page: newPage,
    }

    inputPage.value = newPage
}

const commitPage = () => {
    const page = Number(inputPage.value)

    if (!Number.isFinite(page)) {
        inputPage.value = model.value.page
        return
    }

    setPage(Math.floor(page))
}

const previousPage = () => {
    if (isFirstPage.value) {
        return
    }

    setPage(model.value.page - 1)
}

const nextPage = () => {
    if (isLastPage.value) {
        return
    }

    setPage(model.value.page + 1)
}
</script>

<style scoped>
.page-input::-webkit-inner-spin-button,
.page-input::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

.page-input {
    -moz-appearance: textfield;
}
</style>