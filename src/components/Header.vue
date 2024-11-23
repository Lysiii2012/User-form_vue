<script setup>
import Logo from "../assets/media/Logo.svg";
import Prev from "../assets/media/prev.svg";
</script>

<template>
  <header>
    <div class="container">
      <a href="/" class="btn-prev">
        <img :src="Prev" alt="" />
      </a>
      <a href="/" class="logo">
        <img :src="Logo" alt="Company Logo" />
      </a>
      <div class="title">Profile</div>
    </div>
  </header>
</template>

<style scoped>
.logo {
  max-width: 318px;
  display: block;
}
.btn-prev {
  max-width: 39px;
  display: block;
  margin-right: 8px;
}
.title {
  font-family: "Aeroport";
  font-size: 48px;
  font-weight: 400;
  line-height: 1;
  margin: 0;
}
header .container {
  display: flex;
  align-self: start;
  gap: 38px;
}
header {
  padding: 15px 0;
}
@media screen and (max-width: 767px) {
  .logo {
    max-width: 200px;
  }
  .title {
    font-size: 24px;
  }
  .btn-prev {
    width: 30px;
  }
  header .container {
    gap: 12px;
    align-self: center;
  }
}
</style>
