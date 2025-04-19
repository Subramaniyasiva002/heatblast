<template>
  <main class="bg-cover bg-center py-10 px-4 md:px-20 font-serif animate-fadeIn"
        :style="{ backgroundImage: `url(${backgroundImage})` }">

    <!-- Title Section -->
    <h1 class="text-2xl sm:text-3xl md:text-4xl font-bold text-white bg-[#000080] py-4 rounded-t-lg text-center shadow-md">
      University Administration
    </h1>

    <!-- Administrator Cards Section -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 font-serif mt-8">
      <div 
        v-for="member in administrator" 
        :key="member.name" 
        class="bg-white rounded-lg shadow-lg overflow-hidden flex flex-col items-center border-4 border-black">
        
        <div class="w-full flex justify-center pt-4">
          <div class="w-40 sm:w-48 md:w-60 h-40 sm:h-48 md:h-60 overflow-hidden">
            <img 
              :src="getPhotoPath(member.image)" 
              :alt="member.name" 
              class="w-full h-full object-contain" />
          </div>
        </div>
        
        <div class="flex-grow flex flex-col justify-center p-4 bg-yellow-300 text-center w-full">
          <h2 class="text-lg sm:text-xl md:text-2xl font-semibold text-black">{{ member.name }}</h2>
          <p class="text-sm sm:text-md md:text-lg text-gray-800">{{ member.position }}</p>
          <p class="text-sm sm:text-md md:text-lg text-gray-800">{{ member.university }}</p>
        </div>
      </div>
    </div>
    
  </main>
</template>

<script>
import administrationData from '@/assets/administrator.json';
import backgroundImage from '@/assets/aurcc_bg.webp';  // Background image path

export default {
  name: 'Registrar',
  data() {
    return {
      administrator: administrationData.administrator,
      backgroundImage: backgroundImage
    };
  },
  methods: {
    getPhotoPath(photo) {
      return new URL(`../assets/${photo}`, import.meta.url).href;
    }
  }
};
</script>

<style scoped>
@keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}

.animate-fadeIn {
  animation: fadeIn 1.5s ease-out forwards;
}
</style>
