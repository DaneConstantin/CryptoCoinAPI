<template>
    <main class="w-full pt-24">
        <div class="container relative z-20 mx-auto grid grid-cols-1 gap-x-4 gap-y-20 py-16 lg:grid-cols-2">
            <div class="flex flex-col items-center justify-center text-center lg:items-start lg:text-left">
                <h1 class="mb-4 text-6xl font-bold xl:text-7xl">Cryptaflux</h1>
                <h2 class="mb-12 text-4xl font-bold text-teal-400  decoration-indigo-400/30 xl:text-5xl">NFT
                    Project</h2>
                <p class="text-md mb-10 font-medium text-gray-300 xl:text-lg">
                    Meet a collection of 1000+ amazing figures
                    with different attributes and styles!
                </p>
                <div class="flex flex-col items-center space-x-4 space-y-4 sm:flex-row sm:space-y-0"><a href="/#">
                        <div
                            class="flex w-fit space-x-2 rounded-2xl bg-gray-600 px-4 py-3 font-semibold shadow-lg transition-all duration-300 hover:-translate-y-[1px] hover:bg-gray-700">
                            <span>Join Discord</span> <svg stroke="currentColor" fill="currentColor" stroke-width="0"
                                viewBox="0 0 640 512" height="24" width="24" xmlns="http://www.w3.org/2000/svg">
                                <path
                                    d="M524.531,69.836a1.5,1.5,0,0,0-.764-.7A485.065,485.065,0,0,0,404.081,32.03a1.816,1.816,0,0,0-1.923.91,337.461,337.461,0,0,0-14.9,30.6,447.848,447.848,0,0,0-134.426,0,309.541,309.541,0,0,0-15.135-30.6,1.89,1.89,0,0,0-1.924-.91A483.689,483.689,0,0,0,116.085,69.137a1.712,1.712,0,0,0-.788.676C39.068,183.651,18.186,294.69,28.43,404.354a2.016,2.016,0,0,0,.765,1.375A487.666,487.666,0,0,0,176.02,479.918a1.9,1.9,0,0,0,2.063-.676A348.2,348.2,0,0,0,208.12,430.4a1.86,1.86,0,0,0-1.019-2.588,321.173,321.173,0,0,1-45.868-21.853,1.885,1.885,0,0,1-.185-3.126c3.082-2.309,6.166-4.711,9.109-7.137a1.819,1.819,0,0,1,1.9-.256c96.229,43.917,200.41,43.917,295.5,0a1.812,1.812,0,0,1,1.924.233c2.944,2.426,6.027,4.851,9.132,7.16a1.884,1.884,0,0,1-.162,3.126,301.407,301.407,0,0,1-45.89,21.83,1.875,1.875,0,0,0-1,2.611,391.055,391.055,0,0,0,30.014,48.815,1.864,1.864,0,0,0,2.063.7A486.048,486.048,0,0,0,610.7,405.729a1.882,1.882,0,0,0,.765-1.352C623.729,277.594,590.933,167.465,524.531,69.836ZM222.491,337.58c-28.972,0-52.844-26.587-52.844-59.239S193.056,219.1,222.491,219.1c29.665,0,53.306,26.82,52.843,59.239C275.334,310.993,251.924,337.58,222.491,337.58Zm195.38,0c-28.971,0-52.843-26.587-52.843-59.239S388.437,219.1,417.871,219.1c29.667,0,53.307,26.82,52.844,59.239C470.715,310.993,447.538,337.58,417.871,337.58Z">
                                </path>
                            </svg>
                        </div>
                    </a><a href="/#">
                        <div
                            class="flex w-fit space-x-2 rounded-2xl bg-teal-600 px-4 py-3 font-semibold shadow-lg shadow-teal-500/20 transition-all duration-300 hover:-translate-y-[1px] hover:bg-teal-700">
                            <span>Shop on Opensea</span> <svg stroke="currentColor" fill="currentColor" stroke-width="0"
                                viewBox="0 0 448 512" height="22" width="22" xmlns="http://www.w3.org/2000/svg">
                                <path
                                    d="M190.5 66.9l22.2-22.2c9.4-9.4 24.6-9.4 33.9 0L441 239c9.4 9.4 9.4 24.6 0 33.9L246.6 467.3c-9.4 9.4-24.6 9.4-33.9 0l-22.2-22.2c-9.5-9.5-9.3-25 .4-34.3L311.4 296H24c-13.3 0-24-10.7-24-24v-32c0-13.3 10.7-24 24-24h287.4L190.9 101.2c-9.8-9.3-10-24.8-.4-34.3z">
                                </path>
                            </svg>
                        </div>
                    </a></div>
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

        <section id="markets" class="relative z-10 mx-auto p-10">
            <h3
                class="container mb-4 text-center text-3xl font-semibold  decoration-indigo-500/80 lg:text-left xl:text-4xl">
                <span class="text-red-600 text-4xl animate-ping pr-1">●</span>Live Market
            </h3>
            <div class="py-2 align-middle xl:max-w-[1350px] xl:mx-auto">
                <CryptoTable :cryptos="cryptos" />
            </div>
        </section>

        <section id="roadmap" class="container relative mx-auto py-12">
            <RoadmapFull :steps="steps" />
        </section>

        <section id="faq" class="container relative mx-auto py-12">
            <FAQHome />
        </section>
    </main>
</template>

<script>
import CryptoTable from "../components/CryptoList.vue";
import NFTCard from "../components/HeroNFT.vue";
import RoadmapFull from "../components/Roadmap.vue";
import FAQHome from "../components/FAQ.vue";

export default {

    name: "HomePage",
    components: {
        CryptoTable,
        NFTCard,
        RoadmapFull,
        FAQHome
    },
    data() {
        return {
            keys: process.env.VUE_APP_COINMARKET_KEY,
            cryptos: [],
            imageSrcTwo: "./images/sunny-bull.png",
            imageSrcOne: "./images/chef-bull.png",
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
            const url = `https://pro-api.coinmarketcap.com/v1/cryptocurrency/listings/latest`;
            await fetch(url, {
                method: "GET",
                headers: {
                    "sec-fetch-mode": "no-cors",
                    "Content-Type": "application/json",
                    'X-CMC_PRO_API_KEY': this.keys,
                },
            }).then(response => response.text())
                .then(text => {
                    var obj = JSON.parse(text);

                    this.cryptos = obj.data;
                    console.log(this.cryptos);
                })



        }
    }

};
</script>
