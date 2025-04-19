<template>
  <div class="w-full">
    <!-- Hero / Title Section (unchanged) -->
    <div class="text-center py-5 bg-blue-500 bg-opacity-90">
      <h1 class="text-xl md:text-3xl font-semibold text-white drop-shadow-lg font-serif">
        Cell Coordinators
      </h1>
    </div>

    <!-- Content Section with Background -->
    <div
      class="p-6 md:p-10 bg-cover bg-center"
      :style="backgroundStyle"
    >
      <div class="grid gap-6 grid-cols-1 md:grid-cols-2 lg:grid-cols-3 font-serif">
        <div
          v-for="director in directors"
          :key="director.name"
          class="bg-white rounded-lg shadow-lg flex flex-col items-center md:p-6 p-4 hover:scale-105 transition duration-300 border-2 border-black"
        >
          <div class="text-center">
            <h2 class="text-sm md:text-xl font-semibold text-blue-600">
              {{ director.name }}
            </h2>
            <p class="text-sm md:text-lg text-gray-800">
              {{ director.centre }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import bgImage from '@/assets/aurcc_bg.webp';
import directorsData from '@/assets/COD.json';

export default {
  name: 'Directors',
  data() {
    return {
      directors: directorsData.centres,
    };
  },
  computed: {
    backgroundStyle() {
      return {
        backgroundImage: `linear-gradient(rgba(255, 255, 255, 0.88), rgba(255, 255, 255, 0.88)), url(${bgImage})`,
        backgroundSize: 'cover',
        backgroundPosition: 'center',
      };
    },
  },
};
</script>

<style scoped>
/* No extra scoped CSS needed due to Tailwind */
</style>
