<template>
  <main class="flex-grow">
    <!-- Hero Section -->
    <section 
      class="bg-cover bg-center relative w-full h-40 sm:h-80 md:h-94 animate-fadeIn" 
      :style="{ 
        backgroundImage: `url(${backgroundImage})`
      }">
      <!-- Dark Overlay -->
      <div class="absolute inset-0 bg-black opacity-20"></div>
      <!-- Title -->
      <div class="flex items-center justify-center h-full relative z-10 px-4">
        <h1 class="md:text-4xl text-xl font-extrabold text-white drop-shadow-lg font-serif text-center animate-slideIn">
          DISTANCE EDUCATION
        </h1>
      </div>
    </section>

    <!-- Details Section -->
    <section class="mx-auto py-6 md:py-12 md:px-10 bg-cover bg-center relative rounded-lg animate-popIn"
             :style="{ backgroundImage: `url(${contentBgImage})` }">
      <div class="bg-white rounded-lg shadow-2xl px-4 md:px-10 py-6 font-serif max-w-5xl mx-auto space-y-6">
        <!-- Description -->
        <div class="bg-white rounded-lg shadow-md p-4 md:p-6 animate-fadeIn">
          <h2 class="text-2xl md:text-3xl font-bold text-black mb-4">Description</h2>
          <p class="text-lg text-gray-800">{{ details.description }}</p>
        </div>

        <!-- Sets -->
        <div class="bg-white rounded-lg shadow-md p-4 md:p-6 animate-fadeIn">
          <h2 class="text-2xl md:text-3xl font-bold text-black mb-4">Sets</h2>
          <p class="text-lg text-gray-800">{{ details.sets }}</p>
        </div>

        <!-- Coordinator -->
        <div class="bg-white rounded-lg shadow-md p-4 md:p-6 animate-fadeIn">
          <h2 class="text-2xl md:text-3xl font-bold text-black mb-4">Coordinator</h2>
          <ul class="text-lg text-gray-800 space-y-1">
            <li><strong>Name:</strong> {{ details.coordinator.name }}</li>
            <li><strong>Position:</strong> {{ details.coordinator.position }}</li>
            <li><strong>Department:</strong> {{ details.coordinator.department }}</li>
            <li><strong>University:</strong> {{ details.coordinator.university }}</li>
            <li><strong>Address:</strong> {{ details.coordinator.address }}</li>
          </ul>
        </div>

        <!-- Specializations -->
        <div class="bg-white rounded-lg shadow-md p-4 md:p-6 animate-fadeIn">
          <h2 class="text-2xl md:text-3xl font-bold text-black mb-4">Specializations</h2>
          <ul class="list-disc pl-6 space-y-1 text-lg text-gray-800">
            <li v-for="spec in details.specialization" :key="spec">{{ spec }}</li>
          </ul>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-4">
      <div class="container mx-auto text-center">
        <p>&copy; {{ currentYear }} Distance Education. All rights reserved.</p>
      </div>
    </footer>
  </main>
</template>

<script>
import details from '../assets/distance education.json';
import backgroundImage from '@/assets/offices.webp';
import contentBgImage from '@/assets/aurcc_bg.webp';

export default {
  data() {
    return {
      details,
      backgroundImage,
      contentBgImage
    };
  },
  computed: {
    currentYear() {
      return new Date().getFullYear();
    }
  }
};
</script>

<style scoped>
/* Animations */
@keyframes slideIn {
  0% { transform: translateY(-20px); opacity: 0; }
  100% { transform: translateY(0); opacity: 1; }
}
@keyframes popIn {
  0% { transform: scale(0.9); opacity: 0; }
  100% { transform: scale(1); opacity: 1; }
}
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.animate-slideIn {
  animation: slideIn 0.6s ease-out forwards;
}
.animate-popIn {
  animation: popIn 0.6s ease-out forwards;
}
.animate-fadeIn {
  animation: fadeIn 1s ease-out forwards;
}

/* Fonts */
.font-serif {
  font-family: 'Georgia', 'Times New Roman', Times, serif;
}
.drop-shadow-lg {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}
</style>
