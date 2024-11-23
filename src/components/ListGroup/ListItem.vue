<script setup>
defineProps({
  name: {
    type: String,
    required: true,
  },
  text: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="list-group card">
    <h3>{{ name }}</h3>
    <div class="list-container">
      <p>{{ text }}</p>
      <button>+</button>
    </div>
  </div>
</template>

<style scoped>
.list-container {
  padding: 53px 32px 32px 44px;
  background: #d9d9d9;
  border-radius: 24px;
  max-width: 500px;
  width: 100%;
  min-width: 300px;
  box-sizing: border-box;
  height: 290px;
  overflow-y: auto;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
}
.card p {
  font-family: "Inter";
  font-size: 32px;
  font-weight: 500;
  text-align: left;
  line-height: 20px;
}
.card button {
  color: #00000080;
  font-size: 66px;
  border: none;
  background: none;
  padding: 0;
  line-height: 0.6;
  margin: 0 0 0 auto;
}
.list-group h3 {
  font-family: "Inter";
  font-size: 48px;
  font-weight: 600;
  line-height: 1;
  margin: 0 0 40px;
}
</style>
