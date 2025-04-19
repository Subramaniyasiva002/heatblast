<template>
  <main class="flex-grow">
    <!-- Hero section -->
    <section
      class="bg-cover md:bg-center relative -z-10 w-full h-48 sm:h-64 md:h-94 animate-fadeIn"
      :style="{ backgroundImage: `url(${backgroundImage})` }"
    >
      <div class="absolute top-0 left-0 w-full h-full bg-[#3c2f25] opacity-50"></div>
      <div class="container mx-auto py-16 text-white px-4 md:px-9 relative z-10 font-serif">
        <h1 class="md:text-4xl text-xl font-bold mb-4 animate-slideIn">{{ data.name }}</h1>
        <p v-if="showDescription" class="md:text-xl mb-8 animate-fadeIn delay-1s">{{ data.description }}</p>
        <button 
          @click="toggleDescription" 
          class="bg-[#fdb827] text-[#23120b] md:px-6 md:py-2 px-4 py-2 rounded-lg transition duration-300 hover:bg-[#e0a829]"
        >
          {{ showDescription ? 'Show Less' : 'Learn More' }}
        </button>
      </div>
    </section>

    <!-- Content section with new background -->
    <section
      class="mx-auto font-serif p-4 md:p-9 bg-cover bg-center"
      :style="{ backgroundImage: `url(${aurccBg})` }"
    >
      <!-- Overview -->
      <div class="bg-white/90 rounded-lg animate-popIn mb-8 shadow-md">
        <h2 class="text-2xl md:text-3xl rounded-t-lg text-center bg-[#4b3b32] font-bold text-[#FFDB58] p-4 animate-fadeInUp">
          Overview
        </h2>
        <p class="text-lg md:text-xl font-medium bg-white/90 p-6 rounded-b-lg animate-fadeIn delay-1s">
          {{ data.description }}
        </p>
      </div>

      <!-- Facilities -->
      <div class="bg-white/90 rounded-lg animate-popIn mb-8 shadow-md">
        <h2 class="text-2xl md:text-3xl text-center bg-[#4b3b32] font-bold p-4 text-[#FFDB58] rounded-t-lg animate-fadeInUp">
          Facilities
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-6 animate-fadeIn delay-1s">
          <!-- Indoor -->
          <div>
            <h3 class="text-lg md:text-xl font-bold mb-2">Indoor Games</h3>
            <ul class="list-disc pl-6">
              <li
                v-for="game in data.facilities.IndoorGames"
                :key="game"
                class="mb-2 text-base md:text-lg font-medium animate-fadeInUp delay-2s"
              >
                {{ game }}
              </li>
            </ul>
          </div>
          <!-- Outdoor -->
          <div>
            <h3 class="text-lg md:text-xl font-bold mb-2">Outdoor Games</h3>
            <ul class="list-disc pl-6">
              <li
                v-for="game in data.facilities.OutdoorGames"
                :key="game"
                class="mb-2 text-base md:text-lg font-medium animate-fadeInUp delay-2s"
              >
                {{ game }}
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Contact -->
      <div class="bg-white/90 rounded-lg animate-popIn shadow-md">
        <h2 class="text-2xl md:text-3xl text-center bg-[#4b3b32] font-bold p-4 text-[#FFDB58] rounded-t-lg animate-fadeInUp">
          Contact Us
        </h2>
        <p class="p-6 text-base md:text-lg font-medium animate-fadeIn delay-1s">
          {{ data.contact_us.Address }}
        </p>
      </div>
    </section>
  </main>
</template>

<script>
import data from '../assets/sports.json';
import backgroundImage from '@/assets/sports.webp';
import aurccBg from '@/assets/aurcc_bg.webp';

export default {
  data() {
    return {
      data: data,
      backgroundImage: backgroundImage,
      aurccBg: aurccBg,
      showDescription: false,
    };
  },
  methods: {
    toggleDescription() {
      this.showDescription = !this.showDescription;
      console.log("Button clicked! Show Description:", this.showDescription);
    }
  }
};
</script>

<style scoped>
@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes fadeInUp {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideIn {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(0);
  }
}

@keyframes popIn {
  0% {
    opacity: 0;
    transform: scale(0.8);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

.animate-fadeIn {
  animation: fadeIn 1.5s ease-out forwards;
}

.animate-slideIn {
  animation: slideIn 1s ease-out forwards;
}

.animate-popIn {
  animation: popIn 1.2s ease-out forwards;
}

.animate-fadeInUp {
  animation: fadeInUp 1.5s ease-out forwards;
}
</style>
