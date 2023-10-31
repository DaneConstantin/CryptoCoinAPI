<template>
    <div class="h-[15rem] w-[11rem] rounded-2xl bg-gray-900 shadow-xl xl:h-[23rem] xl:w-[18rem]">
        <div class="relative h-[11rem] xl:h-[18rem] w-full ">
            <img :src="img" alt="Back Card" class="absolute inset-0 w-full h-full object-cover rounded-t-2xl" />
        </div>
        <div class="flex h-[4rem] xl:h-[5rem] w-full items-center justify-between px-4">
            <div class="flex items-center space-x-3">
                <div class="relative h-6 w-6 xl:h-8 xl:w-8">
                    <img :src="img" class="absolute inset-0 w-full h-full object-cover" alt="NFT image" />
                </div>
                <div>
                    <p class="text-xs text-gray-300 xl:text-sm">#{{ id }}</p>
                    <p class="text-md font-medium text-indigo-300 xl:text-xl">{{ price }} ETH</p>
                </div>
            </div>
            <a target="_blank" href="https://opensea.io/">
                <div
                    class="hidden xl:flex w-fit space-x-2 rounded-2xl bg-teal-600 px-4 py-3 text-sm font-semibold shadow-lg shadow-teal-500/20 transition-all duration-300 hover:bg-teal-700">
                    Buy Now
                </div>
            </a>
        </div>
    </div>
</template>
  
<script>
export default {
    name: "NFTCard",
    props: {
        img: String,
        id: String,
        price: Number,
    },
};
</script>
  