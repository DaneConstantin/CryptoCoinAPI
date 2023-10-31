<template>
    <h3 class="mb-8 text-center text-3xl font-semibold text-white lg:text-left xl:text-4xl ">
        Roadmap
    </h3>
    <div class="relative flex flex-col space-y-4 px-4 lg:px-0">
        <div class="absolute left-1/2 z-40 h-full mt-4 w-2 rounded-full bg-indigo-300/60 blur-md lg:left-11">
        </div>
        <div v-for="(step, index) in steps" :key="index"
            class="flex flex-col lg:flex-row items-center rounded-xl bg-gray-900 px-4 py-6 shadow-lg hover:shadow-2xl transition duration-300">
            <div class="rounded-full bg-teal-600 px-6 text-xl font-semibold text-white shadow-teal-500/30">
                <span>{{ index + 1 }}</span>
            </div>
            <div class="ml-3">
                <h3 class="mb-2 text-center text-2xl font-semibold lg:text-left">{{ step.title }}</h3>
                <p class="text-center text-gray-300 lg:text-left">{{ step.description }}</p>
            </div>
        </div>
    </div>
</template>
  
<script>
export default {
    name: "RoadmapFull",
    props: {
        steps: Array,
    },
};
</script>
  