<template>
  <div id="app">
    <!-- Header / Navbar -->
    <header>
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/services">Services</RouterLink>
      </nav>
    </header>

    <!-- Main content -->
    <main>
      <RouterView />
    </main>
  </div>
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<style>
/* Reset & global styles */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background: #1e1e1e;
  color: white;
  line-height: 1.6;
}

/* App container */
#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  display: block; /* normal flow */
}

/* Navbar */
header {
  background: #2c3e50;
  padding: 1rem 2rem;
  border-radius: 8px;
  margin-bottom: 2rem;
}

nav {
  display: flex;
  gap: 20px;
}

nav a {
  color: #42b983;
  text-decoration: none;
  font-weight: bold;
  transition: 0.3s;
}

nav a.router-link-exact-active {
  color: #ffffff;
}

nav a:hover {
  color: #ffffff;
}

/* Main content */
main {
  width: 100%; /* full width for flex inside child components */
  display: block;
}

/* Links & colors */
a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
  padding: 3px;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

/* Remove previous conflicting grid/flex for large screens */
@media (min-width: 1024px) {
  body {
    display: block;
  }

  #app {
    display: block;
    max-width: 1280px;
    margin: 0 auto;
    padding: 2rem;
  }
}
</style>