<script setup lang="ts">
import { onMounted, ref, watch } from 'vue'
import Notify from './SVG/Notify.vue'
import Open from './SVG/Open.vue'

const disclaimerEnabled = ref(false)

function DisableDisclaimer() {
    disclaimerEnabled.value = false

    localStorage.setItem('disclaimer-time', (Date.now() + 604800000).toString())
}

onMounted(() => {
    const time = Number(localStorage.getItem('disclaimer-time')) || Date.now()

    if (time > Date.now()) return

    disclaimerEnabled.value = true
})

watch(disclaimerEnabled, (value) => {
    const intent = value ? 'add' : 'remove'

    document.body.classList[intent]('overflow-hidden')
})
</script>

<template>
    <div
        v-if="disclaimerEnabled"
        class="absolute top-0 left-0 grid place-items-center w-screen h-screen bg-black/50 p-8"
    >
        <div class="p-4 bg-white w-full max-w-sm rounded text-sm">
            <Notify />

            <p>
                This is a redesign, not the actual website for Professional Tax
                Service. All rights are to their respected owners.
            </p>

            <br />

            <p>Click "Actual site" to view the actual website.</p>

            <br />

            <div class="flex justify-end gap-2 whitespace-nowrap">
                <a
                    href="https://www.professionaltaxbg.com"
                    class="text-brand-blue p-2 w-fit font-bold tracking-widest rounded-sm hover:bg-opacity-90 flex"
                >
                    Actual site

                    <Open class="w-3 h-3" />
                </a>

                <button
                    class="bg-brand-blue text-white px-4 py-2 w-fit font-bold tracking-widest rounded-sm hover:bg-opacity-90"
                    @click="DisableDisclaimer"
                >
                    Remind me later
                </button>
            </div>
        </div>
    </div>
</template>
