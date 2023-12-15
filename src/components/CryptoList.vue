<template>
    
    <table class="block text-sm  text-gray-300 w-[calc(100vw-82px)] lg:w-[1000px] divide-y divide-gray-200 overflow-x-auto xl:overflow-x-hidden mx-auto table-fixed">
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
        <tbody class="divide-y divide-gray-300 ">
            <template v-for="(crypto, index) in displayedCryptos" :key="index">
                <tr :class="index % 2 === 0 ? 'bg-black bg-opacity-20 h-[60px]' : ' h-[60px]'" @click="toggleOpen(index, crypto.id)">
                    <td class="p-4 w-[50px]">
                        {{ crypto.market_cap_rank }}
                    </td>
                    <td class="p-4 w-[50px]">
                        <img :src="crypto.image" style="width: 50px;" />
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">{{ crypto.name }}</td>
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
                <tr v-if="openRow === index">

                    <td :colspan="2" class="w-[50px]">
                        <p class="text-lg  px-6 py-3">{{ crypto.name }} <br> Info:</p>
                    </td>
                   
                    <td >
                        <div class="flex flex-col space-y-2 px-4 py-3">
                            <p class="text-gray-400">All Time High:<br> ${{ formatPrice(crypto.ath) }}</p>
                            <p class="text-gray-400">All Time High Date:<br> {{ formatDate(crypto.ath_date) }}</p>
                        </div>
                    </td>
                    <td >
                        <div class="flex flex-col space-y-2 px-4 py-3">
                            <p class="text-gray-400">All Time Low: <br>${{ formatPrice(crypto.atl) }}</p>
                            <p class="text-gray-400">All Time Low Date:<br> {{ formatDate(crypto.atl_date) }}</p>
                        </div>
                    </td>
                    <td >
                        <div class="flex flex-col space-y-2 px-4 py-3">
                            <p class="text-gray-400">24h High: <br>${{ formatPrice(crypto.high_24h) }}</p>
                            <p class="text-gray-400">24h Low:<br> ${{ crypto.low_24h }}</p>
                        </div>
                    </td>
                    <td >
                        <div class="flex flex-col space-y-2 px-4 py-3">
                            <p class="text-gray-400">Price Change 24h:<br> ${{ formatPrice(crypto.price_change_24h) }}</p>
                            <p class="text-gray-400">Change Percentage 24h:<br> {{ formatPrice(crypto.price_change_percentage_24h) }}%
                            </p>
                        </div>
                    </td>
                    <td :colspan="2">
                        <div class="flex flex-col space-y-2 px-4 py-3">
                            <p class="text-gray-400">Market Cap Change 24h:<br> ${{ formatPrice(crypto.market_cap_change_24h) }}</p>
                            <p class="text-gray-400">Market Cap Change Percentage 24h:<br> {{ formatPrice(crypto.market_cap_change_percentage_24h) }}%
                            </p>
                        </div>
                    </td>
                </tr>

            </template>
        </tbody>
    </table>
  
    <ul class="flex justify-center text-base  py-8">
        <button @click="previousPage" :disabled="currentPage === 1">
            <PaginationButton drawing="M5 1 1 5l4 4" />
        </button>
        <span
            class="flex items-center justify-center px-4 h-10 leading-tight text-gray-400 border rounded-lg  bg-gray-900  border-none  hover:bg-gray-700 ">
            Page {{ currentPage }} of {{ totalPages }}
        </span>
        <button @click="nextPage" :disabled="currentPage === totalPages">
            <PaginationButton drawing="m1 9 4-4-4-4" />
        </button>
    </ul>
</template>

<script>
import PaginationButton from './componentsUI/PaginationButtons.vue'
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
    components: {
        PaginationButton
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
        toggleOpen(index) {
            this.openRow = this.openRow === index ? null : index;


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
        formatDate(inputDate) {
            const date = new Date(inputDate);
            const year = date.getFullYear();
            const month = (date.getMonth() + 1).toString().padStart(2, '0');
            const day = date.getDate().toString().padStart(2, '0');

            return `${year}/${month}/${day}`;
        },
        formatBoolean(value) {
            return value ? 'Yes' : 'No';
        }
    }
};
</script>
