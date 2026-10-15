<template>
    <div class="w-full">
        <div ref="captureArea">
            <slot />
        </div>

        <div
            class="fixed bottom-4 left-1/2 -translate-x-1/2 z-[9999] flex items-center gap-3 px-3 py-2 bg-[#f1e3bd]/95 border border-[#756737]/60 shadow-[0_4px_16px_rgba(49,24,12,0.3)]">
            <button v-if="!isRecording" type="button"
                class="whitespace-nowrap px-4 py-2 bg-[#3f472c] text-[#f1e3bd] font-bold rounded-sm"
                @click="startRecording">
                Покрени снимање
            </button>

            <button v-else type="button"
                class="whitespace-nowrap px-4 py-2 bg-[#8b2f24] text-[#f1e3bd] font-bold rounded-sm"
                @click="stopRecording">
                Заустави снимање
            </button>

            <a v-if="recordedUrl" :href="recordedUrl" :download="fileName"
                class="whitespace-nowrap px-4 py-2 border border-[#756737]/60 text-[#312905] font-bold rounded-sm">
                Преузми видео
            </a>
        </div>

        <p v-if="errorMessage"
            class="fixed bottom-20 left-1/2 -translate-x-1/2 z-[9999] w-[calc(100%-32px)] max-w-md px-4 py-2 text-center text-sm font-bold text-[#8b2f24] bg-[#f1e3bd] border border-[#8b2f24]/30 shadow-md">
            {{ errorMessage }}
        </p>
    </div>
</template>

<script setup lang="ts">
import { onBeforeUnmount, ref } from "vue"

const props = withDefaults(
    defineProps<{
        fileName?: string
    }>(),
    {
        fileName: "recording.webm",
    }
)

const captureArea = ref<HTMLElement | null>(null)

const isRecording = ref(false)
const recordedUrl = ref("")
const errorMessage = ref("")

let recorder: MediaRecorder | null = null
let captureStream: MediaStream | null = null
let recordedChunks: Blob[] = []

const startRecording = async () => {
    if (!captureArea.value) {
        return
    }

    errorMessage.value = ""

    if (recordedUrl.value) {
        URL.revokeObjectURL(recordedUrl.value)
        recordedUrl.value = ""
    }

    try {
        const displayMediaOptions = {
            video: {
                displaySurface: "browser",
            },
            audio: false,
            preferCurrentTab: true,
            selfBrowserSurface: "include",
        }

        captureStream = await navigator.mediaDevices.getDisplayMedia(
            displayMediaOptions as DisplayMediaStreamOptions
        )

        const track = captureStream.getVideoTracks()[0]

        const CropTargetApi = (
            window as typeof window & {
                CropTarget?: {
                    fromElement: (element: HTMLElement) => Promise<unknown>
                }
            }
        ).CropTarget

        const cropTrack = track as MediaStreamTrack & {
            cropTo?: (cropTarget: unknown) => Promise<void>
        }

        if (!CropTargetApi || !cropTrack.cropTo) {
            captureStream.getTracks().forEach((streamTrack) => streamTrack.stop())

            errorMessage.value = "Овај прегледач не подржава снимање само изабраног дела странице."
            return
        }

        const cropTarget = await CropTargetApi.fromElement(captureArea.value)

        await cropTrack.cropTo(cropTarget)

        recordedChunks = []

        const mimeType = MediaRecorder.isTypeSupported("video/webm;codecs=vp9")
            ? "video/webm;codecs=vp9"
            : "video/webm"

        recorder = new MediaRecorder(captureStream, {
            mimeType,
        })

        recorder.ondataavailable = (event) => {
            if (event.data.size > 0) {
                recordedChunks.push(event.data)
            }
        }

        recorder.onstop = () => {
            const blob = new Blob(recordedChunks, {
                type: "video/webm",
            })

            recordedUrl.value = URL.createObjectURL(blob)

            captureStream?.getTracks().forEach((streamTrack) => streamTrack.stop())

            captureStream = null
            recorder = null
            isRecording.value = false
        }

        track.addEventListener("ended", () => {
            if (recorder?.state === "recording") {
                recorder.stop()
            }

            isRecording.value = false
        })

        recorder.start(1000)

        isRecording.value = true
    } catch (error) {
        captureStream?.getTracks().forEach((streamTrack) => streamTrack.stop())

        captureStream = null
        recorder = null
        isRecording.value = false

        if (error instanceof DOMException && error.name === "NotAllowedError") {
            errorMessage.value = "Снимање није дозвољено."
            return
        }

        errorMessage.value = "Није могуће покренути снимање."
    }
}

const stopRecording = () => {
    if (!recorder || recorder.state !== "recording") {
        return
    }

    recorder.stop()
}

onBeforeUnmount(() => {
    if (recordedUrl.value) {
        URL.revokeObjectURL(recordedUrl.value)
    }

    captureStream?.getTracks().forEach((track) => track.stop())
})
</script>

<style scoped></style>