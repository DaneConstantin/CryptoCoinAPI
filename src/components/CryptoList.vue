<template>
    <table class="text-sm text-gray-300 min-w-full divide-y divide-gray-200 overflow-x-auto xl:overflow-x-hidden">
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
        <tbody class="divide-y divide-gray-300">
            <template v-for="(crypto, index) in displayedCryptos" :key="index">
                <tr :class="index % 2 === 0 ? 'bg-black bg-opacity-20' : ''" @click="toggleOpen(index, crypto.id)">
                    <td class="pl-4">
                        {{ crypto.market_cap_rank }}
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
                <tr :colspan="7" v-if="openRow === index" class="m-8">
                    <td>
                       
                    </td>
                    <td>
                        <img :src="crypto.image" alt="Coin Image" class="w-16 h-16">
                    </td>
                    <td>
                        <p class="text-lg font-bold">{{ crypto.name }} ({{ crypto.symbol }})</p>
                    </td>

                    <td>
                        <div class="flex items-center space-x-2">
                            <p class="text-gray-500">Current Price: {{ crypto.current_price }}</p>
                            <p class="text-gray-500">Market Cap: {{ crypto.market_cap }}</p>
                        </div>
                    </td>
                    <td>
                        <div class="flex items-center space-x-2">
                            <p class="text-gray-500">24h High: {{ crypto.high_24h }}</p>
                            <p class="text-gray-500">24h Low: {{ crypto.low_24h }}</p>
                        </div>
                    </td>
                    <td>
                        <div class="flex items-center space-x-2">
                            <p class="text-gray-500">Price Change 24h: {{ crypto.price_change_24h }}</p>
                            <p class="text-gray-500">Change Percentage 24h: {{ crypto.price_change_percentage_24h }}%
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
        formatBoolean(value) {
            return value ? 'Yes' : 'No';
        }
    }
};
</script>
