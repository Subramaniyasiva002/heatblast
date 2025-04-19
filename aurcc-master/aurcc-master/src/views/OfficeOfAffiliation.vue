<template>
  <main class="flex-grow">
    <!-- Hero section -->
    <section 
      class="bg-cover bg-center relative w-full h-40 sm:h-80 md:h-94 animate-fadeIn" 
      :style="{ 
        backgroundImage: `url(${backgroundImage})`
      }">
      <!-- Gradient Overlay -->
      <div class="absolute inset-0 bg-black opacity-20"></div>
      
      <!-- Content Container -->
      <div class="flex items-center justify-center h-full relative z-10 px-4">
        <h1 class="md:text-4xl text-xl font-extrabold text-white drop-shadow-lg font-serif text-center animate-slideIn">
          OFFICE OF AFFILIATION
        </h1>
      </div>
    </section>

    <!-- Vertical Tabs Section with Dynamic Content -->
    <section 
      class="mx-auto py-6 md:py-12 md:px-10 rounded-lg animate-popIn"
      :style="{ backgroundImage: `url(${backgroundImageContent})`, backgroundSize: 'cover' }">
      <div class="relative flex flex-col md:px-8 px-4 md:flex-row">
        <!-- Vertical Tabs -->
        <div class="px-8 md:px-0">
          <div class="flex-shrink-0 w-full h-max md:w-64 bg-gradient-to-r from-[#21209c] to-blue-600 rounded-lg shadow-lg p-4 mb-4 md:mb-0 md:mr-4">
            <div class="relative p-4 rounded-lg">
              <h2 class="text-2xl font-serif text-center text-white font-semibold">Sections</h2>
            </div>
            <div class="space-y-2 font-serif">
              <button @click="activeTab = 'Description'" 
                      :class="{'bg-yellow-400 text-[#23120b]': activeTab === 'Description', 'bg-gray-100': activeTab !== 'Description'}" 
                      class="w-full py-2 px-4 rounded-md font-semibold hover:bg-yellow-400 hover:text-[#23120b]">Description</button>
              <button @click="activeTab = 'officeBearer'" 
                      :class="{'bg-yellow-400 text-[#23120b]': activeTab === 'officeBearer', 'bg-gray-100': activeTab !== 'officeBearer'}" 
                      class="w-full py-2 px-4 rounded-md font-semibold hover:bg-yellow-400 hover:text-[#23120b]">Office Bearer</button>
              <button @click="activeTab = 'affiliationStaff'" 
                      :class="{'bg-yellow-400 text-[#23120b]': activeTab === 'affiliationStaff', 'bg-gray-100': activeTab !== 'affiliationStaff'}" 
                      class="w-full py-2 px-4 rounded-md font-semibold hover:bg-yellow-400 hover:text-[#23120b]">Affiliation Administration Staff</button>
              <button @click="activeTab = 'contactUs'" 
                      :class="{'bg-yellow-400 text-[#23120b]': activeTab === 'contactUs', 'bg-gray-100': activeTab !== 'contactUs'}" 
                      class="w-full py-2 px-4 rounded-md font-semibold hover:bg-yellow-400 hover:text-[#23120b]">Contact Us</button>
            </div>
          </div>
        </div>

        <!-- Tab Content Section -->
        <div class="w-full px-0 md:px-10 font-serif min-h-[400px] max-h-[600px] md:max-h-[800px] overflow-y-auto">
          <!-- Description Tab -->
          <div v-if="activeTab === 'Description'" class="bg-white rounded-lg shadow-lg p-4 md:p-6 mb-16 animate-fadeIn">
            <h3 class="text-2xl md:text-3xl font-bold text-black mb-4">Description</h3>
            <p class="text-base text-lg md:text-xl rounded-b-lg mb-8 text-black">{{ data.description['About Office of Affiliation and its activities'] }}</p>        
          </div>

          <!-- Office Bearer Tab -->
          <div v-if="activeTab === 'officeBearer'" class="bg-white rounded-lg shadow-lg p-4 md:p-6 mb-16 animate-fadeIn">
            <h3 class="text-2xl md:text-3xl font-bold text-black mb-4">Office Bearer</h3>
            <div v-if="data.office_bearers" class="text-base md:text-xl text-gray-900">
              <div class="bg-white p-4 rounded-lg shadow-md mb-4">
                <p><strong>Name:</strong> {{ data.office_bearers.name }}</p>
                <p><strong>Qualification:</strong> {{ data.office_bearers.qualification }}</p>
                <p><strong>Position:</strong> {{ data.office_bearers.position }}</p>
              </div>
            </div>
          </div>

          <!-- Affiliation Administration Staff Tab -->
          <div v-if="activeTab === 'affiliationStaff'" class="bg-white rounded-lg shadow-lg p-4 md:p-6 mb-16 animate-fadeIn">
            <h3 class="text-2xl md:text-3xl font-bold text-black mb-4">Affiliation Administration Staff</h3>
            <div v-if="data.affiliation_administration_staff" class="text-base md:text-xl text-gray-900">
              <div v-for="staff in data.affiliation_administration_staff" :key="staff.name" class="bg-white p-4 rounded-lg shadow-md mb-4">
                <p><strong>Name:</strong> {{ staff.name }}</p>
                <p><strong>Position:</strong> {{ staff.position }}</p>
                <p><strong>Phone:</strong> {{ staff.phone }}</p>
                <p><strong>Email:</strong> {{ staff.email }}</p>
              </div>
            </div>
          </div>

          <!-- Contact Us Tab -->
          <div v-if="activeTab === 'contactUs'" class="bg-white rounded-lg shadow-lg p-4 md:p-6 mb-16 animate-fadeIn">
            <h3 class="text-2xl md:text-3xl font-bold text-black mb-4">Contact Us</h3>
            <div v-if="data.contact_details" class="text-base md:text-xl text-gray-900">
              <div class="bg-white p-4 rounded-lg shadow-md">
                <p><strong>Office:</strong> {{ data.contact_details.office }}</p>
                <p><strong>Address:</strong> {{ data.contact_details.address }}</p>
                <p><strong>Phone:</strong> {{ data.contact_details.phone }}</p>
                <p><strong>Email:</strong> {{ data.contact_details.email }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import data from '../assets/office of affiliation.json'; // Your data file
import backgroundImage from '@/assets/offices.webp'; // Hero section background image
import backgroundImageContent from '@/assets/aurcc_bg.webp'; // Content section background image

export default {
  data() {
    return {
      data: data,
      backgroundImage: backgroundImage,
      backgroundImageContent: backgroundImageContent,
      activeTab: 'Description' // Default active tab
    };
  }
};
</script>

<style scoped>
/* Custom styles for responsive layout */
body {
  font-family: 'Arial', sans-serif;
}

/* Add keyframes for animations */
@keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}

@keyframes fadeInUp {
  0% { opacity: 0; transform: translateY(20px); }
  100% { opacity: 1; transform: translateY(0); }
}

@keyframes popIn {
  0% { opacity: 0; transform: scale(0.8); }
  100% { opacity: 1; transform: scale(1); }
}

@keyframes slideIn {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(0); }
}

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
