<template>
    <main class="w-full pt-24">
        <div class="container relative z-20 mx-auto grid grid-cols-1 gap-x-4 gap-y-20 py-16 lg:grid-cols-2">
            <div class="flex flex-col items-center justify-center text-center lg:items-start lg:text-left">
                <h1 class="mb-4 text-6xl font-bold xl:text-7xl">Cryptaflux</h1>
                <h2 class="mb-12 text-4xl font-bold text-teal-400  decoration-indigo-400/30 xl:text-5xl">Blockchain Project
                </h2>
                <p class="text-md mb-10 font-medium text-gray-300 xl:text-lg">
                    Meet a collection of 1000+ amazing figures
                    with different attributes and styles!
                </p>
                <HeroButtons />
            </div>
            <div class="ml-10 flex justify-center">
                <div class="relative -skew-y-3 mt-24 z-10 skew-x-6">
                    <NFTCard :img="imageSrcOne" id="8258" price="1.48" />
                </div>
                <div class="relative skew-y-3 -translate-x-20 animate-pulse -skew-x-6">
                    <NFTCard :img="imageSrcTwo" id="1155" price="1.09" />
                </div>

            </div>
        </div>

        <section id="markets" class="relative z-10 mx-auto px-10">
            <h3
                class="container mb-4 text-center text-3xl font-semibold  decoration-indigo-500/80 lg:text-left xl:text-4xl">
                <span class="text-red-600 text-4xl animate-ping pr-1">●</span>Live Market
            </h3>
            <div class="py-2 align-middle  xl:mx-auto">
                <div v-if="cryptos === null">

                    <p>Loading...</p>
                </div>
                <div v-else class="flex flex-col items-center justify-center ">

                    <CryptoTable :cryptos="cryptos" />
                </div>
            </div>
        </section>

        <section id="roadmap" class="container relative mx-auto py-8">
            <RoadmapFull :steps="steps" />
        </section>

        <section id="faq" class="container relative mx-auto py-8">
            <FAQHome />
        </section>
    </main>
</template>

<script>
import CryptoTable from "../components/CryptoList.vue";
import NFTCard from "../components/HeroNFT.vue";
import RoadmapFull from "../components/Roadmap.vue";
import FAQHome from "../components/FAQ.vue";
import HeroButtons from "../components/componentsUI/HeroButtons.vue";

export default {

    name: "HomePage",
    components: {
        CryptoTable,
        NFTCard,
        RoadmapFull,
        FAQHome,
        HeroButtons
    },
    data() {
        return {

            cryptos: null,
            imageSrcTwo: "./images/NFTTwo.png",
            imageSrcOne: "./images/NFTOne.png",
            steps: [
                {
                    title: "20% ETH Donation",
                    description: "Short description of the roadmap and the step ONE",
                },
                {
                    title: "Sending ETH to other projects",
                    description: "Short description of the roadmap and the step TWO",
                },
                {
                    title: "All NFTs Sold",
                    description: "Short description of the roadmap and the step TWO",
                }

            ]
        }
    },

    created() {

        this.fetchData();
    },
    methods:
    {

        async fetchData() {
            try {
                const url = `https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&sparkline=false&locale=en`;

                const response = await fetch(url);
                const json = await response.json();
                this.cryptos = json;
            } catch (error) {
                console.error("Error fetching data:", error);

            }

        }
    }

};
</script>
