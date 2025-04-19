<template>
	<main class="flex-grow">
	  <!-- Hero Section -->
	  <section 
      class="bg-cover bg-center relative w-full h-40 sm:h-80 md:h-94 animate-fadeIn" 
      :style="{ 
        backgroundImage: `url(${backgroundImage})`
      }">
      <!-- Dark overlay -->
        <div class="absolute inset-0 bg-black opacity-20"></div>
        
        <!-- Centered text -->
        <div class="flex items-center justify-center h-full relative z-10 px-4">
          <h1 class="md:text-4xl text-xl font-extrabold text-white drop-shadow-lg font-serif text-center animate-slideIn">
            EXAM CELL
          </h1>
        </div>
    </section>

	  <!-- Content Sections with Vertical Tabs -->
	  <section 
		class="relative w-full py-6 md:py-12 px-4 md:px-8 animate-fadeInUp bg-cover bg-center"
		:style="{ backgroundImage: `url(${aurccBg})` }">
		<div class="flex flex-col md:flex-row gap-6">
		  <!-- Vertical Tabs -->
		  <div class="md:w-1/4 w-full bg-gradient-to-r from-[#21209c] to-blue-600 rounded-2xl shadow-xl p-4">
			<div class="text-center mb-6">
			  <h2 class="text-2xl font-serif text-white font-semibold">Sections</h2>
			</div>
			<div class="space-y-2">
			  <button @click="currentSection = 'about'"
				  :class="{'bg-yellow-400 text-[#23120b]': currentSection === 'about', 'bg-white text-black': currentSection !== 'about'}"
				  class="w-full py-2 px-4 rounded-xl font-semibold transition-colors duration-300 hover:bg-yellow-400 hover:text-[#23120b]">
				About
			  </button>
			  <button @click="currentSection = 'services'"
				  :class="{'bg-yellow-400 text-[#23120b]': currentSection === 'services', 'bg-white text-black': currentSection !== 'services'}"
				  class="w-full py-2 px-4 rounded-xl font-semibold transition-colors duration-300 hover:bg-yellow-400 hover:text-[#23120b]">
				Services
			  </button>
			  <button @click="currentSection = 'office_bearers'"
				  :class="{'bg-yellow-400 text-[#23120b]': currentSection === 'office_bearers', 'bg-white text-black': currentSection !== 'office_bearers'}"
				  class="w-full py-2 px-4 rounded-xl font-semibold transition-colors duration-300 hover:bg-yellow-400 hover:text-[#23120b]">
				Office Bearers
			  </button>
			</div>
		  </div>

		  <!-- Tab Content -->
		  <div class="md:w-3/4 w-full">
			<transition name="fade" mode="out-in">
			  <div v-if="currentSection === 'about'" key="about" class="bg-white rounded-2xl shadow-xl p-6 animate-fadeInUp">
				<h2 class="text-2xl md:text-3xl font-bold text-black mb-4">About the Exam Cell</h2>
				<p class="text-base md:text-lg">{{ data.description }}</p>
			  </div>
			  <div v-else-if="currentSection === 'services'" key="services" class="bg-white rounded-2xl shadow-xl p-6 animate-fadeInUp">
				<h2 class="text-2xl md:text-3xl font-bold text-black mb-4">Services</h2>
				<ul class="list-disc pl-5 space-y-2">
				  <li v-for="service in data.services" :key="service" class="text-base md:text-lg">{{ service }}</li>
				</ul>
			  </div>
			  <div v-else-if="currentSection === 'office_bearers'" key="office_bearers" class="bg-white rounded-2xl shadow-xl p-6 animate-fadeInUp">
				<h2 class="text-2xl md:text-3xl font-bold text-black mb-4">Office Bearers</h2>
				<ul class="list-disc pl-5 space-y-2">
				  <li v-for="bearer in data.office_bearers" :key="bearer.name" class="text-base md:text-lg">
					<strong>{{ bearer.position }}:</strong> {{ bearer.name }}
				  </li>
				</ul>
			  </div>
			</transition>
		  </div>
		</div>
	  </section>
	</main>
</template>

<script>
import data from '../assets/exam-cell.json';
import backgroundImage from '@/assets/offices.webp';
import aurccBg from '@/assets/aurcc_bg.webp';

export default {
  data() {
	return {
	  data: data,
	  backgroundImage: backgroundImage,
	  aurccBg: aurccBg,
	  currentSection: 'about', // Default tab
	};
  }
};
</script>

<style>
body {
  font-family: 'Arial', sans-serif;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>