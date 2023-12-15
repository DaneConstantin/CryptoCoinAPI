<template>
    <a
        class="flex items-center justify-center px-4 h-10 ml-0 leading-tight text-gray-400 border  rounded-lg  bg-gray-900  border-none  hover:bg-gray-700 hover:text-white">
        <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 6 10">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="drawing" />
        </svg>
    </a>
</template>
<script>
export default {
    name: "PaginationButton",
    props: {
        drawing: String,
    },

}
</script>