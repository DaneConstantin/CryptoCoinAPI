<template>
    <div class="overflow-x-auto xl:overflow-x-hidden">
        <table class="text-sm text-gray-300 min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-800 text-md font-medium">
                <tr>
                    <th></th>
                    <th scope="col" class="px-6 py-3 text-left tracking-wider"></th>
                    <th scope="col" class="px-6 py-3 text-left tracking-wider">Name</th>
                    <th scope="col" class="px-6 py-3 text-left tracking-wider">Symbol</th>
                    <th scope="col" class="px-6 py-3 text-left tracking-wider">Price (USD)</th>
                    <th scope="col" class="px-6 py-3 text-left tracking-wider">24h Change</th>
                    <th scope="col" class="px-6 py-3 text-left tracking-wider">24h %</th>
                    <th scope="col" class="px-6 py-3 text-left tracking-wider">Market Cap</th>
                    <th scope="col" class="px-6 py-3 text-left tracking-wider">Max Supply</th>
                </tr>
            </thead>
            <tbody class="divide-y divide-gray-200">


                <template v-for="(crypto, index) in displayedCryptos" :key="index">
                    <tr :class="index % 2 === 0 ? 'bg-black bg-opacity-20' : ''" @click="toggleOpen(index, crypto.id)">
                        <td :class="index % 2 === 0 ? 'bg-black bg-opacity-20' : ''">

                            <div class="pl-4">
                                {{ crypto.market_cap_rank }}
                            </div>

                        </td>
                        <td class="pl-4">
                            <img :src="crypto.image" style="width: 30px;" />
                        </td>
                        <td class="flex px-6 py-4 whitespace-nowrap">{{ crypto.name }}</td>
                        <td class="px-6 py-4 whitespace-nowrap uppercase">{{ crypto.symbol }}</td>
                        <td class="px-6 py-4 whitespace-nowrap">${{ formatPrice(crypto.current_price) }}</td>
                        <td class="px-6 py-4 whitespace-nowrap">{{ formatPrice(crypto.price_change_24h) }}
                        </td>
                        <td
                            :class="crypto.price_change_percentage_24h > 0 ? 'text-green-700 font-bold px-6 py-4 whitespace-nowrap' : 'text-red-700 font-bold px-6 py-4 whitespace-nowrap'">
                            {{
                                formatPrice(crypto.price_change_percentage_24h) }}%</td>

                        <td class="px-6 py-4 whitespace-nowrap">${{ formatBigNumber(crypto.market_cap)
                        }}
                        </td>

                        <td class="px-6 py-4 whitespace-nowrap">{{ crypto.max_supply ? formatPrice(crypto.max_supply) : '∞'
                        }}
                        </td>
                    </tr>
                    <tr v-if="openRow === index && coininfo">
                        <div class="flex flex-wrap gap-4 p-8">
                            <div class="flex flex-shrink-0">
                                <img :src="coininfo[0]?.image" alt="Coin Image" class="w-16 h-16">
                                <p class="text-lg font-bold">{{ coininfo[0].name }} ({{ coininfo[0].symbol }})</p>
                            </div>
                            <div class="flex-grow">

                                <div class="flex items-center space-x-2">
                                    <p class="text-gray-500">Current Price: {{ coininfo[0].current_price }}</p>
                                    <p class="text-gray-500">Market Cap: {{ coininfo[0].market_cap }}</p>
                                </div>
                                <div class="flex items-center space-x-2">
                                    <p class="text-gray-500">24h High: {{ coininfo[0].high_24h }}</p>
                                    <p class="text-gray-500">24h Low: {{ coininfo[0].low_24h }}</p>
                                </div>
                                <div class="flex items-center space-x-2">
                                    <p class="text-gray-500">Price Change 24h: {{ coininfo[0].price_change_24h }}
                                    </p>
                                    <p class="text-gray-500">Change Percentage 24h: {{
                                        coininfo[0].price_change_percentage_24h }}%</p>
                                </div>
                            </div>
                        </div>
                    </tr>

                </template>
            </tbody>
        </table>

    </div>

    <div class=" py-4">
        <ul class="flex justify-center -space-x-px h-10 text-base">
            <button @click="previousPage" :disabled="currentPage === 1">
                <a
                    class="flex items-center justify-center px-4 h-10 ml-0 leading-tight text-gray-400 border  rounded-l-lg  bg-gray-900  border-none  hover:bg-gray-700 hover:text-white">
                    <span class="sr-only">Previous</span>
                    <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none"
                        viewBox="0 0 6 10">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M5 1 1 5l4 4" />
                    </svg>
                </a>
            </button>
            <span
                class="flex items-center justify-center px-4 h-10 leading-tight text-gray-400 border  bg-gray-900  border-none  hover:bg-gray-700 ">
                Page {{ currentPage }} of {{ totalPages }}</span>
            <button @click="nextPage" :disabled="currentPage === totalPages">
                <a
                    class="flex items-center justify-center px-4 h-10 leading-tight text-gray-400 border  rounded-r-lg  bg-gray-900  border-none  hover:bg-gray-700 hover:text-white">
                    <span class="sr-only">Next</span>
                    <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none"
                        viewBox="0 0 6 10">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="m1 9 4-4-4-4" />
                    </svg>
                </a>
            </button>
        </ul>


    </div>
</template>

<script>
export default {
    name: "CryptoTable",
    props: {
        cryptos: String,
    },
    data() {
        return {
            openRow: null,
            itemsPerPage: 10,
            currentPage: 1,
            coininfo: null
        };
    },
    computed: {
        totalPages() {
            return Math.ceil(this.cryptos.length / this.itemsPerPage);
        },
        displayedCryptos() {
            const startIndex = (this.currentPage - 1) * this.itemsPerPage;
            const endIndex = startIndex + this.itemsPerPage;
            return this.cryptos.slice(startIndex, endIndex);
        },
    },

    methods: {
        toggleOpen(index, crypto) {
            this.openRow = this.openRow === index ? null : index;
            if (this.openRow) {
                this.fetchData(crypto);
            }

        },
        async fetchData(coinId) {
            try {
                const url = `https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&ids=${coinId}&x_cg_api_key=CG-LB7JofPBFMu7ZreiHyfmHrJx`;
                const response = await fetch(url);
                this.coininfo = await response.json([0]);


            } catch (error) {
                console.error("Error fetching data:", error);

            }

        },
        previousPage() {
            if (this.currentPage > 1) {
                this.currentPage--;
            }
        },
        nextPage() {
            if (this.currentPage < this.totalPages) {
                this.currentPage++;
            }
        },
        formatBigNumber(price) {
            if (price >= 1000000) {
                return (price / 1000000).toFixed(0).replace(/\B(?=(\d{3})+(?!\d))/g, '.') + 'M';
            } else if (price >= 1000) {
                return (price / 1000).toFixed(0).replace(/\B(?=(\d{3})+(?!\d))/g, '.') + 'k';
            }
            return price.toFixed(2);

        },
        formatPrice(price) {

            if (typeof price === 'number') {
                return price.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, '.');
            }
            return price;
        },
        formatBoolean(value) {
            return value ? 'Yes' : 'No';
        }
    }
};
</script>
