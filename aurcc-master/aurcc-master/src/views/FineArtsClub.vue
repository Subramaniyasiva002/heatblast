<template>
  <main class="flex-grow">
    <!-- Hero section -->
    <section 
      class="bg-cover md:bg-center relative -z-10 w-full h-48 sm:h-64 md:h-94 animate-fadeIn" 
      :style="{ 
        backgroundImage: `url(${backgroundImage})`, 
        backgroundSize: 'cover',
        backgroundPosition: 'top center' 
      }"
    >
      <div class="absolute top-0 left-0 w-full h-full bg-black opacity-20"></div>
      <div class="container mx-auto py-16 md:py-24 text-white px-6 md:px-28 relative z-10 font-serif">
        <h1 class="md:text-4xl text-xl font-bold animate-slideIn">Fine Arts Club</h1>
      </div>
    </section>

    <!-- Main Content Section -->
    <section
      class="py-12 px-4 md:px-16 bg-cover bg-center space-y-10 font-serif animate-fadeIn"
      :style="{ backgroundImage: `url(${aurccBackground})` }"
    >
      <!-- Description Section -->
      <div class="bg-white bg-opacity-90 rounded-lg shadow-xl animate-popIn">
        <h1 class="text-2xl md:text-3xl font-bold mb-4 bg-[#000080] text-white p-4 text-center rounded-t-lg">
          LAYAM AAM RHYTHM OF ARTS MUSIC & DANCE
        </h1>
        <p class="text-lg md:text-xl font-medium leading-relaxed p-6">
          {{ description }}
        </p>
      </div>

      <!-- Office Bearers Section -->
      <div class="bg-white bg-opacity-90 rounded-lg shadow-lg animate-fadeIn delay-1s">
        <h2 class="text-2xl md:text-3xl font-bold mb-4 bg-[#000080] text-white p-4 text-center rounded-t-lg">
          Office Bearers
        </h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6 p-6 font-medium">
          <div
            v-for="bearer in officeBearers"
            :key="bearer['SL.NO']"
            class="bg-gray-100 rounded-md p-4 shadow-inner animate-fadeInUp delay-1s"
          >
            <p><strong>Name:</strong> {{ bearer.Name }}</p>
            <p><strong>Designation:</strong> {{ bearer.Designation }}</p>
            <p><strong>Department:</strong> {{ bearer.Department }}</p>
          </div>
        </div>
      </div>

      <!-- Coordinator Section -->
      <div class="bg-white bg-opacity-90 rounded-lg shadow-lg animate-fadeIn delay-2s">
        <h2 class="text-2xl md:text-3xl font-bold mb-4 bg-[#000080] text-white p-4 text-center rounded-t-lg">
          Coordinator
        </h2>
        <div class="p-6 font-medium space-y-2 animate-popIn delay-2s">
          <p class="text-lg"><strong>Name:</strong> {{ coordinator.Name }}</p>
          <p class="text-lg"><strong>Designation:</strong> {{ coordinator.Designation }}</p>
          <p class="text-lg"><strong>Department:</strong> {{ coordinator.Department }}</p>
          <p class="text-lg"><strong>University:</strong> {{ coordinator.University }}</p>
          <p class="text-lg"><strong>Address:</strong> {{ coordinator.Address }}</p>
          <p class="text-lg"><strong>Mobile:</strong> {{ coordinator.Mobile }}</p>
          <p class="text-lg">
            <strong>Email:</strong> 
            <a :href="`mailto:${coordinator.Email}`" class="text-blue-500 underline">
              {{ coordinator.Email }}
            </a>
          </p>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import data from '../assets/fine arts.json';
import backgroundImage from '@/assets/fac.webp';
import aurccBackground from '@/assets/aurcc_bg.webp';

export default {
  data() {
    return {
      backgroundImage,
      aurccBackground,
      description: data.description,
      officeBearers: data.office_bearers,
      coordinator: data.Coordinator
    };
  }
};
</script>

<style scoped>
/* Animations */
@keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}

@keyframes fadeInUp {
  0% { opacity: 0; transform: translateY(20px); }
  100% { opacity: 1; transform: translateY(0); }
}

@keyframes popIn {
  0% { opacity: 0; transform: scale(0.95); }
  100% { opacity: 1; transform: scale(1); }
}

@keyframes slideIn {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(0); }
}

/* Utility classes */
.animate-fadeIn {
  animation: fadeIn 1.5s ease-out forwards;
}
.animate-popIn {
  animation: popIn 1.2s ease-out forwards;
}
.animate-fadeInUp {
  animation: fadeInUp 1.5s ease-out forwards;
}
.animate-slideIn {
  animation: slideIn 1s ease-out forwards;
}
</style>
