<template>
  <div>
   <!-- Navbar -->
<nav class="bg-[#042e68] text-white px-4 py-3 flex justify-between items-center shadow-md">
  <h1 class="text-xl font-semibold">College Faculty Finder</h1>
</nav>
  <div class="text-sm flex items-center">
    Block:
    <select
      v-model="selectedBlock"
      class="ml-2 p-1 rounded text-black focus:outline-none focus:ring-2 focus:ring-blue-500"
    >
      <option value="ALL">ALL</option>
      <option>A1</option>
      <option>B1</option>
      <option>B2</option>
      <option>B3</option>
      <option>B4</option>
      <option>C1</option>
      <option>C2</option>
      <option>C3</option>
    </select>
  </div>


    <!-- Main container -->
    <div class="p-4 bg-gray-100 min-h-screen pb-16">
      <!-- Search bar -->
      <input
  v-model="searchTerm"
  placeholder="Search by name or e-code"
  class="p-2 border rounded w-full mb-4 focus:outline-none focus:ring-2 focus:ring-blue-500"
  style="padding: 0.6rem 4.2rem; font-size: medium;"
>


      <!-- Faculty cards -->
      <div
        v-for="faculty in filteredFaculty"
        :key="faculty.ecode"
        class="border p-3 mb-2 rounded shadow bg-white transition-all duration-300 ease-in-out"
      >
        <!-- Header row with name and toggle icon -->
        <div
          class="flex justify-between items-center cursor-pointer"
          @click="toggleDetails(faculty.ecode)"
        >
        <h2 class="text-lg font-bold text-blue-700 flex items-center">
  <i class="fas fa-user-tie mr-2"></i>{{ faculty.name }}
  <span class="text-blue-500 font-normal ml-2">({{ faculty.ecode }})</span>
</h2>

          <i
            :class="detailsVisible[faculty.ecode] ? 'fas fa-chevron-up' : 'fas fa-chevron-down'"
            class="text-gray-500"
          ></i>
        </div>

        <!-- Details section -->
        <transition name="fade">
  <div v-if="detailsVisible[faculty.ecode]" class="mt-2 text-gray-600 ml-2">
    <p>Seating: {{ faculty.seating }}</p>
    <p>Email:
      <a
        :href="'mailto:' + faculty.email"
        class="text-blue-500 hover:underline"
      >
        {{ faculty.email }}
      </a>
    </p>
    <p>Phone: {{ faculty.contact }}</p>
  </div>
</transition>

      </div>
    </div>

    <!-- Fixed footer -->
    <footer class="fixed bottom-0 w-full text-center bg-blue-800 text-white py-2">
      Made by Nikhil Sharma
    </footer>
  </div>
</template>

<script>
import { facultyList } from "../data/faculty.js";

export default {
  data() {
    return {
      searchTerm: "",
      selectedBlock: "ALL",
      faculty: facultyList,
      detailsVisible: {},
    };
  },
  computed: {
    filteredFaculty() {
      const term = this.searchTerm.toLowerCase();
      return this.faculty.filter((f) => {
        const matchesSearch =
          f.name.toLowerCase().includes(term) || f.ecode.toLowerCase().includes(term);
        const matchesBlock =
          this.selectedBlock === "ALL" || f.seating.includes(this.selectedBlock);
        return matchesSearch && matchesBlock;
      });
    },
  },
  methods: {
    toggleDetails(ecode) {
      this.detailsVisible[ecode] = !this.detailsVisible[ecode];
    },
  },
};
</script>

<style scoped>
/* Include Font Awesome */
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css");

/* Navbar styling */
/* (Optional) nav styles if needed without Tailwind */
nav {
  background-color: #042e68;
    color: white;
    padding: 0rem 1rem;
    display: flex;
    font-size: x-large;
}



/* Smooth transition for details */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* Footer styling */
footer {
  position:fixed;
  bottom: 0;
  width: 100%;
  text-align: center;
  background-color: #042e68; /* Blue background */
  color: white; /* White text */
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}

/* Faculty card hover effect */
.border:hover {
  box-shadow: 0px 4px 10px rgb(246, 154, 154);
}
</style>
