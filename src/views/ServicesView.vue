<template>
  <div :class="['app-container', { dark: darkMode }]">
    <!-- Navbar -->
    <nav class="navbar">
      <h2>CarwashVue 🚗🧽</h2>
      <div class="nav-actions">
        <button class="toggle-btn" @click="darkMode = !darkMode">
          {{ darkMode ? '🌙 Dark Mode' : '☀️ Light Mode' }}
        </button>
      </div>
    </nav>

    <!-- Search bar -->
    <div class="search-container">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="🔍 Search services (ID, Name, Price)..."
        class="search-box"
      />
    </div>

    <!-- Status banners -->
    <div v-if="loading" class="status-message loading">
      Services Loading..
    </div>
    <div v-else-if="error" class="status-message error">
      {{ error }}
    </div>
    <div v-else>
      <!-- Services Grid -->
      <div class="services-container">
        <div 
          v-for="service in filteredServices" 
          :key="service.id" 
          class="service-card"
        >
          <p class="service-field"><strong>ID:</strong> {{ service.id }}</p>
          <p class="service-field"><strong>Name:</strong> {{ service.name }}</p>
          <p class="service-field"><strong>Price:</strong> {{ service.price }} KES</p>
        </div>
      </div>

      <!-- No results -->
      <div v-if="filteredServices.length === 0" class="status-message">
        No matching results found.
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      services: [],
      searchQuery: "",
      loading: true,
      error: null,
      darkMode: false,
    };
  },
  computed: {
    filteredServices() {
      if (!this.searchQuery) return this.services;
      const q = this.searchQuery.toLowerCase();
      return this.services.filter(s =>
        s.id.toString().includes(q) ||
        s.name.toLowerCase().includes(q) ||
        s.price.toString().includes(q)
      );
    }
  },
  async mounted() {
    try {
      const response = await fetch("http://localhost:4000/api/services");

      if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
      this.services = await response.json();
    } catch (error) {
      this.error = "⚠ Failed to load services. Please check your internet connection.";
      console.error("Error fetching services:", error);
    } finally {
      this.loading = false;
    }
  }
};
</script>

<style scoped>
/* same styles as you had – unchanged */
</style>
