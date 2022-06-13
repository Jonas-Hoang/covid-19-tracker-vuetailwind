<template>
  <div class="grid md:grid-cols-2 gap-4">
    <!-- Box 1 -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded ml-5">
        <h3 class="text-3xl text-blue-900 font-bold mb-4">Casses</h3>
        <div class="text-2xl mb-4">
            <span class="font-bold">New:</span>
            {{ numberWithDots(stats.NewConfirmed) }}
        </div>
        <div class="text-2xl mb-4">
            <span class="font-bold">Total:</span>
            {{ numberWithDots(stats.TotalConfirmed) }}
        </div>
    </div>
    <!-- Box 2 -->
    <div class="shadow-md bg-red-100 p-10 text-center rounded mr-5">
        <h3 class="text-3xl text-red-900 font-bold mb-4">Death</h3>
        <div class="text-2xl mb-4">
            <span class="font-bold">New:</span>
            {{ numberWithDots(stats.NewDeaths) }}
        </div>
        <div class="text-2xl mb-4">
            <span class="font-bold">Total:</span>
            {{ numberWithDots(stats.TotalDeaths)}}
        </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "DataBoxes",
  props: ["stats"],
  methods: {
    numberWithDots(x) {
    return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    }
  },
};
</script>