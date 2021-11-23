<template>
  <div class="loader spinner-border text-success" role="status">
  </div>
  <div class="loading">
    <p>Loading....</p>
  </div>
</template>
<script>
export default {
  name: "Loader",
};
</script>
<style scoped>
.loader {
  position: fixed;
  top: 45%;
  left: 50%;
}
.loading {
  position: fixed;
  top: 49%;
  left: 48%;
  color:#198754;
  font-size: 25px;
  font-weight: 600;
}
</style>