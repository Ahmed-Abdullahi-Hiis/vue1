<!-- <template>
  <header class="navbar">
    <nav>
      <RouterLink to="/" class="link">Home</RouterLink>
      <RouterLink to="/about" class="link">About</RouterLink>
      <RouterLink to="/services" class="link">Services</RouterLink>
    </nav>
    <button @click="toggleDarkMode" class="dark-btn">
      {{ isDark ? "🌙 Dark" : "☀️ Light" }}
    </button>
  </header>
</template>

<script setup>
import { ref, onMounted } from "vue";

const isDark = ref(false);

function toggleDarkMode() {
  isDark.value = !isDark.value;
  document.body.classList.toggle("dark", isDark.value);
}

onMounted(() => {
  if (document.body.classList.contains("dark")) {
    isDark.value = true;
  }
});
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: var(--nav-bg);
  padding: 1rem;
}

.link {
  margin-right: 15px;
  text-decoration: none;
  color: var(--text-color);
  font-weight: bold;
}

.link:hover {
  text-decoration: underline;
}

.dark-btn {
  padding: 0.4rem 0.8rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

/* Light Mode */
:root {
  --nav-bg: #f5f5f5;
  --text-color: #222;
  --bg-color: #fff;
}

/* Dark Mode */
body.dark {
  --nav-bg: #222;
  --text-color: #f5f5f5;
  --bg-color: #121212;
}

body {
  background: var(--bg-color);
  color: var(--text-color);
  margin: 0;
}
</style> -->
