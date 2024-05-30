<template>
  <nav>
    <div class="logo">
      <img src="../assets/logo.svg" alt="Logo" width="100" height="100" @click="home" />
    </div>
  </nav>
</template>

<script>
  export default {
    name: "Navbar",
    methods: {
      home() {
        location.href = "/";
      },
    },
  };
</script>

<style scoped>
	nav {
    background-color: #06283D;
    width: 100%;
  }

  .logo {
    display: grid;
    place-items: center;
  }

  .logo img {
    cursor: pointer;
  }
</style>