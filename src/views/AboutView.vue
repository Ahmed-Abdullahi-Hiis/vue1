<template>
  <div class="about">
    <h1 v-if="isLoginedIn">This is an About page</h1>
    <h1 v-else>You are not logged in</h1>
    <p>Welcome to CarwashVue 🚗🧽</p>
    <!-- <h1>{{ isLoginedIn ? 'Welcome back' : 'you are not logged in' }}</h1> -->
  </div>
</template>

<script>
export default {
  data() {
    return{
      isLoginedIn: true,
    }
  },
}

</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
}
</style>