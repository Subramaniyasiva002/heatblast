<template>
  <main class="flex-grow bg-cover bg-center py-10 px-4 md:px-20 font-serif animate-fadeIn"
        :style="{ backgroundImage: `url(${backgroundImage})` }">
    
    <!-- Heading -->
    <h2 class="text-2xl md:text-4xl font-bold text-white bg-[#000080] rounded-t-xl text-center py-4 shadow-lg">
      ORGANOGRAM
    </h2>

    <!-- PDF Viewer -->
    <div class="bg-white bg-opacity-90 p-4 md:p-6 rounded-b-xl shadow-2xl overflow-auto">
      <iframe :src="pdfUrl" class="w-full h-[70vh] md:h-[90vh] rounded-md shadow-md border border-gray-300"></iframe>
    </div>
    
  </main>
</template>

<script>
import OrganogramPdf from '@/assets/Organogram.pdf';
import backgroundImage from '@/assets/aurcc_bg.webp';

export default {
  data() {
    return {
      pdfUrl: OrganogramPdf,
      backgroundImage: backgroundImage,
    };
  },
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
