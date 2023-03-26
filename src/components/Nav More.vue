<script setup lang="ts">
import { ref, reactive, onMounted } from 'vue'
import links from './Nav Links.js'

const windowSize = reactive({ width: 0, height: 0 })
const moreEnabled = ref(false)

onMounted(() => {
    function updateWindowSize() {
        windowSize.width = window.innerWidth
        windowSize.height = window.innerHeight
    }

    window.onresize = updateWindowSize

    updateWindowSize()
})
</script>

<template>
    <button
        class="h-full grid place-items-center aspect-square md:hidden"
        @click="moreEnabled = true"
    >
        <svg
            width="24"
            height="24"
            fill="none"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
        >
            <path
                d="M12 8a2 2 0 1 1 0-4 2 2 0 0 1 0 4ZM12 14a2 2 0 1 1 0-4 2 2 0 0 1 0 4ZM10 18a2 2 0 1 0 4 0 2 2 0 0 0-4 0Z"
                fill="#fff"
            />
        </svg>
    </button>

    <div
        class="fixed top-0 left-0 flex justify-end items-start p-2 px-6 pointer-events-none md:hidden"
        :style="{
            width: windowSize.width + 'px',
            height: windowSize.height + 'px',
        }"
    >
        <div
            class="py-4 bg-brand-blue text-white border border-white/25 rounded shadow-blue-900/15 shadow-lg transition duration-200 flex flex-col gap-2 relative"
            :class="
                moreEnabled
                    ? ' pointer-events-auto'
                    : 'transform scale-75 translate-x-4 -translate-y-4 opacity-0 pointer-events-none'
            "
        >
            <button
                class="h-8 w-8 p-2 absolute grid place-items-center top-2 right-2"
                @click="moreEnabled = false"
            >
                <svg
                    width="24"
                    height="24"
                    fill="none"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                    class="h-full w-full"
                >
                    <path
                        d="m4.21 4.387.083-.094a1 1 0 0 1 1.32-.083l.094.083L12 10.585l6.293-6.292a1 1 0 1 1 1.414 1.414L13.415 12l6.292 6.293a1 1 0 0 1 .083 1.32l-.083.094a1 1 0 0 1-1.32.083l-.094-.083L12 13.415l-6.293 6.292a1 1 0 0 1-1.414-1.414L10.585 12 4.293 5.707a1 1 0 0 1-.083-1.32l.083-.094-.083.094Z"
                        fill="#fff"
                    />
                </svg>
            </button>

            <a
                v-for="link of links"
                :key="link.href"
                :href="link.href"
                class="px-4 hover:underline"
            >
                {{ link.text }}
            </a>
        </div>
    </div>
</template>
