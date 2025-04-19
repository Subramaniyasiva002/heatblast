<template>
  <div class="flex-grow">
    <!-- Hero Section -->
    <section 
      class="bg-cover bg-center relative w-full h-40 sm:h-80 md:h-94 animate-fadeIn" 
      :style="{ backgroundImage: `url(${backgroundImage})` }"
    >
      <!-- Dark overlay -->
      <div class="absolute inset-0 bg-black opacity-20"></div>
      <!-- Centered text -->
      <div class="flex items-center justify-center h-full relative z-10 px-4">
        <h1 class="md:text-4xl text-xl font-extrabold text-white drop-shadow-lg font-serif text-center animate-slideIn">
          RESEARCH CELL
        </h1>
      </div>
    </section>

    <!-- Content Section with aurcc_bg background -->
    <section 
      class="relative w-full bg-cover bg-no-repeat bg-center py-6 md:py-12 px-4 md:px-10 animate-popIn"
      :style="{ backgroundImage: `url(${backgroundImageContent})` }"
    >
      <div class="flex flex-col md:flex-row gap-4">
        <!-- Vertical Tabs -->
        <div class="flex-shrink-0 w-full md:w-64 bg-gradient-to-r from-[#21209c] to-blue-600 rounded-2xl shadow-xl p-4">
          <div class="text-center text-white font-serif text-2xl font-semibold mb-4">Sections</div>
          <div class="space-y-2">
            <button @click="currentSection = 'Description'" 
                    :class="{'bg-yellow-400 text-[#23120b]': currentSection === 'Description', 'bg-gray-100': currentSection !== 'Description'}" 
                    class="w-full py-2 px-4 rounded-md font-semibold hover:bg-yellow-400 hover:text-[#23120b]">Description</button>
            <button @click="currentSection = 'Supervisors'" 
                    :class="{'bg-yellow-400 text-[#23120b]': currentSection === 'Supervisors', 'bg-gray-100': currentSection !== 'Supervisors'}" 
                    class="w-full py-2 px-4 rounded-md font-semibold hover:bg-yellow-400 hover:text-[#23120b]">Supervisors</button>
            <button @click="currentSection = 'PhD Scholars'" 
                    :class="{'bg-yellow-400 text-[#23120b]': currentSection === 'PhD Scholars', 'bg-gray-100': currentSection !== 'PhD Scholars'}" 
                    class="w-full py-2 px-4 rounded-md font-semibold hover:bg-yellow-400 hover:text-[#23120b]">PhD Scholars</button>
            <button @click="currentSection = 'PG Projects'" 
                    :class="{'bg-yellow-400 text-[#23120b]': currentSection === 'PG Projects', 'bg-gray-100': currentSection !== 'PG Projects'}" 
                    class="w-full py-2 px-4 rounded-md font-semibold hover:bg-yellow-400 hover:text-[#23120b]">PG Projects</button>
            <button @click="currentSection = 'Stipend Details'" 
                    :class="{'bg-yellow-400 text-[#23120b]': currentSection === 'Stipend Details', 'bg-gray-100': currentSection !== 'Stipend Details'}" 
                    class="w-full py-2 px-4 rounded-md font-semibold hover:bg-yellow-400 hover:text-[#23120b]">Stipend Details</button>
          </div>
        </div>

        <!-- Dynamic Content -->
        <div class="w-full min-h-[400px] max-h-[600px] md:max-h-[800px] overflow-y-auto animate-fadeIn">
          <div v-if="currentSection === 'Description'" class="bg-white rounded-2xl shadow-xl p-6">
            <h2 class="text-2xl md:text-3xl font-bold text-black mb-4">Description</h2>
            <p class="text-base md:text-lg text-black">{{ data.description }}</p>
          </div>

          <div v-else-if="currentSection === 'Supervisors'" class="bg-white rounded-2xl shadow-xl p-6">
            <h2 class="text-2xl md:text-3xl font-bold text-black mb-4">Supervisors</h2>
            <ul class="list-disc pl-4 text-base md:text-lg">
              <li v-for="supervisor in data.supervisors" :key="supervisor">{{ supervisor }}</li>
            </ul>
          </div>

          <div v-else-if="currentSection === 'PhD Scholars'" class="bg-white rounded-2xl shadow-xl p-6">
            <h2 class="text-2xl md:text-3xl font-bold text-black mb-4">PhD Scholars</h2>
            <p class="text-base md:text-xl">Total PhD Scholars: {{ data.phd_scholars.total }}</p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-4">
              <div class="bg-gray-50 rounded-md p-4 shadow-md">
                <h3 class="text-lg font-semibold mb-2">Faculty-wise</h3>
                <a :href="data.phd_scholars.faculty_wise" target="_blank" class="text-blue-600 hover:underline">View Faculty-wise PhD Scholars</a>
              </div>
              <div class="bg-gray-50 rounded-md p-4 shadow-md">
                <h3 class="text-lg font-semibold mb-2">Department-wise</h3>
                <a :href="data.phd_scholars.department_wise" target="_blank" class="text-blue-600 hover:underline">View Department-wise PhD Scholars</a>
              </div>
            </div>
          </div>

          <div v-else-if="currentSection === 'PG Projects'" class="bg-white rounded-2xl shadow-xl p-6">
            <h2 class="text-2xl md:text-3xl font-bold text-black mb-4">PG Projects</h2>
            <p class="text-base md:text-xl">Total PG Projects: {{ data.pg_projects.total }}</p>
            <table class="w-full mt-4 text-sm md:text-base">
              <thead class="bg-gray-200">
                <tr>
                  <th class="px-4 py-2 text-left">Department</th>
                  <th class="px-4 py-2 text-left">Number of Projects</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(projects, department) in data.pg_projects.departmentwise" :key="department">
                  <td class="border px-4 py-2">{{ department }}</td>
                  <td class="border px-4 py-2">{{ projects }}</td>
                </tr>
              </tbody>
            </table>
          </div>

          <div v-else-if="currentSection === 'Stipend Details'" class="bg-white rounded-2xl shadow-xl p-6">
            <h2 class="text-2xl md:text-3xl font-bold text-black mb-4">Stipend Details</h2>
            <div class="overflow-x-auto">
              <table class="w-full text-sm md:text-base">
                <thead class="bg-gray-800 text-white">
                  <tr>
                    <th class="px-4 py-2">Supervisor Name</th>
                    <th class="px-4 py-2">Scholar Name</th>
                    <th class="px-4 py-2">Mode</th>
                    <th class="px-4 py-2">Batch</th>
                    <th class="px-4 py-2">Funding Agency</th>
                    <th class="px-4 py-2">Funding Scheme</th>
                    <th class="px-4 py-2">Stipend Amount</th>
                    <th class="px-4 py-2">Stipend Duration</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="detail in data.stipend_details" :key="detail.scholar_name">
                    <td class="border px-4 py-2">{{ detail.supervisor_name }}</td>
                    <td class="border px-4 py-2">{{ detail.scholar_name }}</td>
                    <td class="border px-4 py-2">{{ detail.full_time_or_part_time }}</td>
                    <td class="border px-4 py-2">{{ detail.batch }}</td>
                    <td class="border px-4 py-2">{{ detail.funding_agency }}</td>
                    <td class="border px-4 py-2">{{ detail.funding_scheme }}</td>
                    <td class="border px-4 py-2">{{ detail.stipend_amount }}</td>
                    <td class="border px-4 py-2">{{ detail.stipend_duration }}</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import data from '../assets/research-cell.json';
import backgroundImage from '@/assets/offices.webp';
import backgroundImageContent from '@/assets/aurcc_bg.webp';

export default {
  data() {
    return {
      backgroundImage: backgroundImage,
      backgroundImageContent: backgroundImageContent,
      currentSection: "Description",
      data: data
    };
  }
};
</script>
