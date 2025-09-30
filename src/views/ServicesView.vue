<template>
  <div class="services-container">
    <div 
      v-for="post in posts" 
      :key="post.id" 
      class="service-card"
    >
      <p class="service-field"><strong>UserID:</strong> {{ post.userId }}</p>
      <p class="service-field"><strong>ID:</strong> {{ post.id }}</p>
      <p class="service-field"><strong>Title:</strong> {{ post.title }}</p>
      <p class="service-field"><strong>Body:</strong> {{ post.body }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [] 
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(data => this.posts = data)
  }
}
</script>

<style scoped>
.services-container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: flex-start;
  padding: 10px;
  width: 100%;
  margin: 0;
  box-sizing: border-box;
}

.service-card {
  flex: 1 1 calc(20% - 10px);
  min-width: 200px;
  background: rgba(18, 18, 225, 1);
  color: #fff;
  border-radius: 10px;
  padding: 10px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.service-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.3);
}

.service-field {
  margin: 6px 0;
  font-size: 14px;
}

@media (max-width: 768px) {
  .service-card { flex: 0 1 45%; }
}

@media (max-width: 480px) {
  .service-card { flex: 0 1 100%; }
}
</style>
