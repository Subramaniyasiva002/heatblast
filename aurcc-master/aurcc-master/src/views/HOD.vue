<template>
  <div class="w-full bg-indigo-100">
    <!-- Title / Hero Section (Unchanged) -->
    <div class="text-center mb-8 py-3 md:py-6 bg-blue-500 bg-opacity-90 font-serif">
      <h1 class="text-xl md:text-3xl font-semibold text-black">Head of the Departments</h1>
    </div>

    <!-- Content Section with Background -->
    <div
      class="bg-cover bg-center bg-no-repeat p-6 md:p-12"
      :style="backgroundStyle"
    >
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 md:gap-10 font-serif">
        <div
          v-for="hod in hods"
          :key="hod.name"
          class="bg-white rounded-lg shadow-xl overflow-hidden flex flex-col m-6 items-center border-4 border-black hover:scale-105 transition"
        >
          <div class="w-full flex justify-center pt-4">
            <div class="md:w-60 md:h-60 w-40 h-40 sm:w-48 sm:h-48 overflow-hidden">
              <img
                :src="getPhotoPath(hod.photo)"
                :alt="hod.name"
                class="w-full h-full object-contain"
              />
            </div>
          </div>
          <div class="flex-grow flex flex-col justify-center p-4 md:p-6 bg-gray-200 text-center w-full">
            <h2 class="text-sm sm:text-lg md:text-2xl font-semibold text-blue-600">{{ hod.name }}</h2>
            <p class="text-xs sm:text-sm md:text-lg text-gray-800">{{ hod.department }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ltImage from '@/assets/aurcc_bg.webp';
import hodsData from '@/assets/HOD.json';

export default {
  name: 'HODs',
  data() {
    return {
      hods: hodsData.departments,
    };
  },
  computed: {
    backgroundStyle() {
      return {
        backgroundImage: `url(${ltImage})`,
        backgroundSize: 'cover',
        backgroundPosition: 'center',
      };
    },
  },
  methods: {
    getPhotoPath(photo) {
      return new URL(`../assets/${photo}`, import.meta.url).href;
    },
  },
};
</script>

<style scoped>
/* For subtle shadow effect on text, if needed */
.text-shadow-lg {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}
</style>
