<template>
  <main class="flex-grow font-serif">
    <!-- Hero Section -->
    <section
      class="relative w-full h-40 sm:h-80 md:h-94 bg-cover bg-center animate-fadeIn"
      :style="{ backgroundImage: `url(${backgroundImage})` }"
    >
      <div class="absolute inset-0 bg-black opacity-20"></div>
      <div class="flex items-center justify-center h-full relative z-10 px-4">
        <h1 class="text-white text-xl md:text-4xl font-extrabold drop-shadow-lg text-center animate-slideIn">
          ZONAL OFFICE
        </h1>
      </div>
    </section>

    <!-- Content Section with Vertical Tabs -->
    <section
      class="mx-auto py-6 md:py-12 md:px-10 bg-cover bg-center relative rounded-lg animate-popIn"
      :style="{ backgroundImage: `url(${aurccBgImage})` }"
    >
      <div class="flex flex-col md:flex-row px-4 md:px-8 relative">
        <!-- Tab Navigation -->
        <aside class="flex-shrink-0 w-full md:w-64 mb-6 md:mb-0 md:mr-6">
          <div class="bg-gradient-to-r from-[#21209c] to-blue-600 rounded-lg shadow-lg p-4">
            <h2 class="text-2xl text-white text-center font-semibold mb-4">Sections</h2>
            <div class="space-y-2">
              <button
                v-for="tab in tabs"
                :key="tab.key"
                @click="activeTab = tab.key"
                :class="[
                  'w-full py-2 px-4 rounded-md font-semibold transition-all duration-200',
                  activeTab === tab.key
                    ? 'bg-yellow-400 text-[#23120b]'
                    : 'bg-white text-gray-800 hover:bg-yellow-400 hover:text-[#23120b]'
                ]"
              >
                {{ tab.label }}
              </button>
            </div>
          </div>
        </aside>

        <!-- Tab Content -->
        <section class="w-full min-h-[400px] max-h-[600px] md:max-h-[800px] overflow-y-auto px-0 md:px-6">
          <!-- Description Tab -->
          <div v-if="activeTab === 'description'" class="bg-white rounded-lg shadow-lg p-4 md:p-6 mb-16 animate-fadeIn">
            <h3 class="text-2xl md:text-3xl font-bold text-black mb-4">Description</h3>
            <ul class="list-disc pl-6 text-lg md:text-xl text-gray-900 font-medium">
              <li v-for="(desc, index) in data.description" :key="index">{{ desc }}</li>
            </ul>
          </div>

          <!-- Zone List PDF Tab -->
          <div v-if="activeTab === 'zoneList'" class="bg-white rounded-lg shadow-lg p-4 md:p-6 mb-16 animate-fadeIn">
            <h3 class="text-2xl md:text-3xl font-bold text-black mb-4">Zone List of Colleges</h3>
            <iframe
              :src="zonalListPDF"
              class="w-full h-[500px] sm:h-[700px] rounded-lg border-2 border-gray-300 shadow-sm"
              frameborder="0"
            ></iframe>
          </div>

          <!-- Office Bearers Tab -->
          <div v-if="activeTab === 'officeBearers'" class="bg-white rounded-lg shadow-lg p-4 md:p-6 mb-16 animate-fadeIn">
            <h3 class="text-2xl md:text-3xl font-bold text-black mb-6">Office Bearers</h3>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div
                v-for="bearer in data['Office bearers']"
                :key="bearer.name"
                class="p-6 bg-white rounded-lg shadow-md"
              >
                <h4 class="text-lg font-semibold text-gray-900">{{ bearer.name }}</h4>
                <p class="text-gray-700">{{ bearer.designation }}</p>
              </div>
            </div>
          </div>
        </section>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-4">
      <div class="text-center container mx-auto">
        <p>&copy; {{ currentYear }} Zonal Office. All rights reserved.</p>
      </div>
    </footer>
  </main>
</template>

<script>
import data from '../assets/zonaloffice.json';
import zonalListPDF from '../assets/zonal-list.pdf';
import backgroundImage from '@/assets/offices.webp';
import aurccBgImage from '@/assets/aurcc_bg.webp';

export default {
  data() {
    return {
      data: data[0],
      backgroundImage,
      aurccBgImage,
      zonalListPDF,
      activeTab: 'description',
      tabs: [
        { key: 'description', label: 'Description' },
        { key: 'zoneList', label: 'Zone List of Colleges' },
        { key: 'officeBearers', label: 'Office Bearers' },
      ],
    };
  },
  computed: {
    currentYear() {
      return new Date().getFullYear();
    },
  },
};
</script>

<style scoped>
/* Font Definitions */
.font-serif {
  font-family: 'Georgia', 'Times New Roman', Times, serif;
}

/* Animations */
@keyframes slideIn {
  0% {
    transform: translateY(-20px);
    opacity: 0;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}

@keyframes popIn {
  0% {
    transform: scale(0.9);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

@media (max-width: 640px) {
  .animate-slideIn {
    animation: slideIn 0.5s ease-in-out;
  }
  .animate-popIn {
    animation: popIn 0.5s ease-in-out;
  }
}

.animate-slideIn {
  animation: slideIn 0.5s ease-in-out;
}
.animate-popIn {
  animation: popIn 0.5s ease-in-out;
}
.animate-fadeIn {
  animation: fadeIn 0.6s ease-in;
}
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
