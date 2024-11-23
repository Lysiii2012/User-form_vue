<template>
  <div>
    <Header />
    <div class="container container-body">
      <ListGroup />
      <Form />
    </div>
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Form from "./components/Form/Form.vue";
import ListGroup from "./components/ListGroup/ListContainer.vue";
</script>

<style scoped>
.container-body {
  padding-top: 82px;
  align-items: center;
}

@media screen and (max-width: 1167px) {
  .container-body {
    display: flex;
    flex-direction: column-reverse;
  }
}
</style>