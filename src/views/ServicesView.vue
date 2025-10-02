<template>
  <div :class="['app-container', { dark: darkMode }]">
    <!-- Dark / Light toggle button -->
    <button class="toggle-btn" @click="darkMode = !darkMode">
      {{ darkMode ? '🌙 Dark Mode' : '☀️ Light Mode' }}
    </button>

    <!-- Search bar -->
    <input
      v-model="searchQuery"
      type="text"
      placeholder="🔍 Search services..."
      class="search-box"
    />

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
          v-for="post in filteredPosts" 
          :key="post.id" 
          class="service-card"
        >
          <p class="service-field"><strong>UserID:</strong> {{ post.userId }}</p>
          <p class="service-field"><strong>ID:</strong> {{ post.id }}</p>
          <p class="service-field"><strong>Title:</strong> {{ post.title }}</p>
          <p class="service-field"><strong>Body:</strong> {{ post.body }}</p>
        </div>
      </div>

      <!-- No results -->
      <div v-if="filteredPosts.length === 0" class="status-message">
        No matching results found.
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
      searchQuery: "",
      loading: true,
      error: null,
      darkMode: false,
    }
  },
  computed: {
    filteredPosts() {
      if (!this.searchQuery) return this.posts;
      const q = this.searchQuery.toLowerCase();
      return this.posts.filter(
        post =>
          post.title.toLowerCase().includes(q) ||
          post.body.toLowerCase().includes(q)
      );
    }
  },
  async mounted() {   
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/posts');
      if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
      this.posts = await response.json();
    } catch (error) {
      this.error = "⚠ Failed to load services. Please check your internet connection."; 
      console.error('Error fetching posts:', error);
    } finally {
      this.loading = false;
    }
  }
}
</script>

<style scoped>
/* App container */
.app-container {
  min-height: 100vh;
  padding: 1rem;
  background: #f4f4f4;
  color: #222;
  transition: background 0.3s, color 0.3s;
}

.app-container.dark {
  background: #121212;
  color: #f4f4f4;
}

/* Toggle button */
.toggle-btn {
  padding: 8px 14px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  margin-bottom: 1rem;
  background: #333;
  color: #fff;
}
.app-container.dark .toggle-btn {
  background: #ddd;
  color: #000;
}

/* Search bar */
.search-box {
  display: block;
  width: 100%;
  max-width: 400px;
  padding: 10px;
  margin-bottom: 1rem;
  border-radius: 8px;
  border: 1px solid #ccc;
  outline: none;
}
.app-container.dark .search-box {
  background: #333;
  color: #fff;
  border: 1px solid #666;
}

/* Status banners */
.status-message {
  width: 100%;
  text-align: center;
  font-size: 1.2rem;
  font-weight: bold;
  padding: 1rem;
  margin: 1rem 0;
  border-radius: 6px;
}

.loading {
  background: #222;
  color: chartreuse;
}

.error {
  background: #300;
  color: crimson;
}

.app-container.dark .loading {
  background: #111;
  color: #90ee90;
}

.app-container.dark .error {
  background: #511;
  color: #ff7b7b;
}

/* Services Grid */
.services-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 15px;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
}

.service-card {
  background: #126;
  color: #fff;
  border-radius: 10px;
  padding: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.service-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.3);
}

/* Dark mode override */
.app-container.dark .service-card {
  background: #222;
  color: #eee;
}

.service-field {
  margin: 6px 0;
  font-size: 14px;
}
</style>
