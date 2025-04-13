<template>
  <div>
    <FacultyList />
  </div>
</template>

<script>
import FacultyList from './components/FacultyList.vue';

export default {
  components: {
    FacultyList
  }
};
</script>

<style>
/* Optional: Custom background color styling */
.bg-blue-100 {
  background-color: #ebf8ff; /* Light blue background */
}
body, html {
  margin: 0;
  padding: 0;
}
</style>
