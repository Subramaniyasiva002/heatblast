<template>
  <main class="flex-grow">
    <!-- Hero Banner -->
    <section
      class="relative w-full h-40 sm:h-80 md:h-94 bg-cover bg-center"
      :style="{ backgroundImage: `url(${backgroundImage})` }"
    >
      <div class="absolute inset-0 bg-black opacity-40"></div>
      <div class="relative z-10 flex items-center justify-center h-full px-4">
        <h1 class="text-white text-2xl md:text-5xl font-extrabold font-serif drop-shadow-lg text-center animate-fadeInDown">
          ENTREPRENEURSHIP DEVELOPMENT CELL
        </h1>
      </div>
    </section>

    <!-- Content Section with Background Image Animated -->
    <section
      class="w-full bg-cover bg-center bg-no-repeat h-full relative z-0"
      :style="{ backgroundImage: `url(${aurccBg})` }"
    >
      <div class="absolute inset-0 bg-black opacity-40"></div> <!-- Background overlay -->

      <div class="relative z-10 py-6 md:py-12 md:px-10">
        <div class="flex">
          <!-- Sidebar Tabs -->
          <aside class="flex-shrink-0 w-full md:w-64 p-4 md:mr-4 bg-gradient-to-r from-[#21209c] to-blue-600 rounded-lg shadow-lg">
            <h2 class="text-white text-2xl font-serif font-semibold text-center mb-4">Sections</h2>
            <div class="space-y-2 font-serif">
              <button
                v-for="tab in tabs"
                :key="tab.key"
                @click="activeTab = tab.key"
                :class="{
                  'bg-yellow-400 text-[#23120b]': activeTab === tab.key,
                  'bg-white text-gray-800': activeTab !== tab.key
                }"
                class="w-full py-2 px-4 rounded-md font-semibold transition-all duration-200 hover:bg-yellow-400 hover:text-[#23120b]"
              >
                {{ tab.label }}
              </button>
            </div>
          </aside>

          <!-- Tab Contents -->
          <section class="flex-grow px-6 py-4 bg-white/80 backdrop-blur-md rounded-xl shadow-2xl animate-popIn">
            <!-- Description -->
            <div v-if="activeTab === 'Description'" class="bg-white rounded-lg shadow-lg p-6 mb-16">
              <h3 class="text-2xl md:text-3xl font-bold mb-4 text-black">Description</h3>
              <p class="text-lg md:text-xl text-black">
                Entrepreneurship is the person who plays a certain price for a product to resell it at an uncertain price, hereby making decisions about obtaining and using the resources while consequently admitting the risk of enterprise.
              </p>
            </div>

            <!-- Objectives -->
            <div v-if="activeTab === 'objectives'" class="bg-white rounded-lg shadow-lg p-6 mb-16">
              <h3 class="text-2xl md:text-3xl font-bold mb-4 text-black">Objectives</h3>
              <ul class="text-lg md:text-xl list-disc pl-6 font-medium text-gray-900">
                <li v-for="objective in data.description.objectives" :key="objective">{{ objective }}</li>
              </ul>
            </div>

            <!-- Key Activities -->
            <div v-if="activeTab === 'key_activities'" class="bg-white rounded-lg shadow-lg p-6 mb-16">
              <h3 class="text-2xl md:text-3xl font-bold mb-4 text-black">Key Activities</h3>
              <div
                v-for="activity in data.description.key_activities"
                :key="activity.name"
                class="p-4 mb-4 rounded-lg bg-gray-100"
              >
                <h4 class="text-xl font-semibold">{{ activity.name }}</h4>
                <p><strong>Location:</strong> {{ activity.location }}</p>
                <p><strong>Details:</strong> {{ activity.details }}</p>
              </div>
            </div>

            <!-- MOU -->
            <div v-if="activeTab === 'mou'" class="bg-white rounded-lg shadow-lg p-6 mb-16">
              <h3 class="text-2xl md:text-3xl font-bold mb-4 text-black">MOU</h3>
              <ul class="text-lg md:text-xl list-disc pl-6 font-medium text-gray-900">
                <li v-for="mou in data.MOU" :key="mou">{{ mou }}</li>
              </ul>
            </div>

            <!-- Links -->
            <div v-if="activeTab === 'links'" class="bg-white rounded-lg shadow-lg p-6 mb-16">
              <h3 class="text-2xl md:text-3xl font-bold mb-4 text-black">Links</h3>
              <ul class="text-lg font-medium text-gray-900 list-disc pl-6">
                <li v-for="link in data.links" :key="link">
                  <a
                    :href="'http://' + link"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="hover:underline"
                  >
                    {{ link }}
                  </a>
                </li>
              </ul>
            </div>

            <!-- Office Bearers -->
            <div v-if="activeTab === 'office_bearers'" class="bg-white rounded-lg shadow-lg p-6 mb-16">
              <h3 class="text-2xl md:text-3xl font-bold mb-4 text-black">Office Bearers</h3>
              <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div
                  v-for="member in data.office_bearers"
                  :key="member.email"
                  class="p-4 bg-gray-100 rounded-lg shadow-md"
                >
                  <p class="text-xl font-bold text-center">{{ member.name }}</p>
                  <p class="text-center"><strong>Position:</strong> {{ member.position }}</p>
                  <p class="text-center">
                    <strong>Email:</strong>
                    <a :href="'mailto:' + member.email">{{ member.email }}</a>
                  </p>
                  <p class="text-center"><strong>Organization:</strong> {{ member.organization }}</p>
                </div>
              </div>
            </div>
          </section>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import data from '../assets/ED-cell.json';
import backgroundImage from '@/assets/offices.webp';
import aurccBg from '@/assets/aurcc_bg.webp';

export default {
  data() {
    return {
      data,
      backgroundImage,
      aurccBg,
      activeTab: 'objectives',
      tabs: [
        { key: 'Description', label: 'Description' },
        { key: 'objectives', label: 'Objectives' },
        { key: 'key_activities', label: 'Key Activities' },
        { key: 'mou', label: 'MOU' },
        { key: 'links', label: 'Links' },
        { key: 'office_bearers', label: 'Office Bearers' }
      ]
    };
  }
};
</script>

<style scoped>
@keyframes fadeInDown {
  0% {
    opacity: 0;
    transform: translateY(-40px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
.animate-fadeInDown {
  animation: fadeInDown 1.2s ease-out;
}

@keyframes popIn {
  0% {
    opacity: 0;
    transform: scale(0.95);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}
.animate-popIn {
  animation: popIn 0.5s ease-in-out;
}
</style>
