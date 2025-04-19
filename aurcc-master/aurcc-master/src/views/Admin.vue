<template>
  <div class="bg-indigo-100 min-h-screen">
    <!-- Title Section -->
    <div class="text-center md:py-6 py-3 bg-blue-500 bg-opacity-90">
      <h1 class="text-xl md:text-3xl font-semibold font-serif text-black">ADMINISTRATIVE STAFF</h1>
    </div>

    <!-- Tabs -->
    <div class="flex justify-center mt-8">
      <div class="flex space-x-4 text-lg md:text-2xl font-semibold">
        <button
          v-for="(section, sectionName) in administrator"
          :key="sectionName"
          :class="[
            'py-2 px-4 rounded-t-lg transition duration-300',
            selectedTab === sectionName ? 'bg-blue-500 text-white' : 'bg-white text-blue-500 hover:bg-blue-200'
          ]"
          @click="selectTab(sectionName)"
        >
          {{ sectionName }}
        </button>
      </div>
    </div>

    <!-- Content -->
    <div
      class="container mx-auto p-6 font-serif bg-cover bg-center bg-no-repeat"
      :style="{ backgroundImage: `url(${backgroundImage})` }"
    >
      <div v-if="selectedTab && administrator[selectedTab]" class="mt-10 min-h-[80vh]">
        <div
          v-for="(subsection, subsectionName) in administrator[selectedTab]"
          :key="subsectionName"
          class="mb-8"
        >
          <h3 class="text-xl md:text-2xl font-bold text-center mb-6 underline underline-offset-4">
            {{ subsectionName.replace('_', ' ') }}
          </h3>

          <!-- Deputy Manager -->
          <div v-if="subsection.DEPUTY_MANAGER" class="mb-8">
            <h4 class="text-lg md:text-2xl font-semibold mb-4 text-center">Deputy Manager</h4>
            <div class="flex justify-center flex-wrap">
              <div
                v-for="member in subsection.DEPUTY_MANAGER"
                :key="member.name"
                class="bg-white rounded-lg shadow-xl m-4 p-4 w-72 border-4 border-black flex flex-col items-center hover:scale-105 transition"
              >
                <div class="w-40 h-40 overflow-hidden">
                  <img
                    :src="getPhotoPath(member.image)"
                    :alt="member.name"
                    class="w-full h-full object-contain"
                  />
                </div>
                <div class="mt-4 text-center bg-yellow-300 p-4 w-full">
                  <h2 class="text-lg font-semibold text-black">{{ member.name }}</h2>
                  <p class="text-gray-800 text-sm">{{ member.position || 'Position not available' }}</p>
                  <p class="text-gray-800 text-sm">{{ member.email || 'Email not available' }}</p>
                </div>
              </div>
            </div>
          </div>

          <!-- Staff Members -->
          <div v-if="subsection.STAFFS">
            <h4 class="text-lg md:text-2xl font-semibold mb-4 text-center">Staff Members</h4>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
              <div
                v-for="member in subsection.STAFFS"
                :key="member.name"
                class="bg-white rounded-lg shadow-xl p-4 border-4 border-black flex flex-col items-center hover:scale-105 transition"
              >
                <div class="w-40 h-40 overflow-hidden">
                  <img
                    :src="getPhotoPath(member.image)"
                    :alt="member.name"
                    class="w-full h-full object-contain"
                  />
                </div>
                <div class="mt-4 text-center bg-yellow-300 p-4 w-full">
                  <h2 class="text-lg font-semibold text-black">{{ member.name }}</h2>
                  <p class="text-gray-800 text-sm">{{ member.position || 'Position not available' }}</p>
                  <p class="text-gray-800 text-sm">{{ member.email || 'Email not available' }}</p>
                </div>
              </div>
            </div>
          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<script>
import administrationData from '@/assets/administration.json';
import backgroundImage from '@/assets/aurcc_bg.webp';

export default {
  name: 'Admin',
  data() {
    return {
      administrator: {},
      selectedTab: ''
    };
  },
  mounted() {
    // Load data and set Admin1 as default once data is ready
    this.administrator = administrationData;
    this.selectedTab = Object.keys(this.administrator)[0]; // Set first tab (Admin1)
  },
  methods: {
    getPhotoPath(photo) {
      return photo ? new URL(`../assets/${photo}`, import.meta.url).href : 'default-image-path.jpg';
    },
    selectTab(tabName) {
      this.selectedTab = tabName;
    }
  },
  computed: {
    backgroundImage() {
      return backgroundImage;
    }
  }
};
</script>

<style scoped>
/* For extra spacing/consistency if needed */
</style>
