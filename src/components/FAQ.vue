<template>
    <h3 class="mb-14 text-center text-3xl font-semibold lg:text-left xl:text-4xl">
        Frequently Asked Questions</h3>
    <div class="w-100 w-full border-none px-4 lg:px-0 space-y-4">
        <dl v-for="(row, id) in rows" :key="id">

            <dt v-on:click="row.open = !row.open"
                :class="{ 'bg-teal-600/80 ': row.open, 'bg-transparent   hover:border-teal-600/80 ': !row.open }"
                class="flex space-between px-4 py-4 bg-teal-600/80 border-2 border-teal-600/30 rounded-2xl cursor-pointer select-none items-center justify-between  text-gray-300 transition duration-300  hover:text-white">
                <h4 class="text-lg font-medium">{{ row.term }}</h4>
                <svg v-if="row.open" stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 448 512"
                    height="22" width="22" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M416 208H32c-17.67 0-32 14.33-32 32v32c0 17.67 14.33 32 32 32h384c17.67 0 32-14.33 32-32v-32c0-17.67-14.33-32-32-32z">
                    </path>
                </svg>
                <svg v-else stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 448 512" height="22"
                    width="22" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M416 208H272V64c0-17.67-14.33-32-32-32h-32c-17.67 0-32 14.33-32 32v144H32c-17.67 0-32 14.33-32 32v32c0 17.67 14.33 32 32 32h144v144c0 17.67 14.33 32 32 32h32c17.67 0 32-14.33 32-32V304h144c17.67 0 32-14.33 32-32v-32c0-17.67-14.33-32-32-32z">
                    </path>
                </svg>
            </dt>

            <dd v-if="row.open" class="bg-transparent text-white border-none px-4 py-4">{{ row.details }}</dd>
        </dl>
    </div>
</template>
  
<script>

export default {
    name: "FAQHome",
    data() {
        return {
            rows: {
                q1: {
                    term: 'Can I buy an NFT from Opensea?',
                    details: 'Cryptaflux is a collection of 1000+ amazing figures with different attributes and styles hosted on Ethereum Blockchain. You can buy these figures on OpenSea.',
                    open: false
                },
                q2: {
                    term: 'How much do they Cost?',
                    details: 'Cryptaflux is a collection of 1000+ amazing figures with different attributes and styles hosted on Ethereum Blockchain. You can buy these figures on OpenSea.',
                    open: false
                },
                q3: {
                    term: 'What is Cryptaflux',
                    details: 'Cryptaflux is a collection of 1000+ amazing figures with different attributes and styles hosted on Ethereum Blockchain. You can buy these figures on OpenSea.',
                    open: false
                }
            }
        }
    },

};
</script>
  