<template>
  <div class="container-fluid">
    <navigasi />
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.card {
  position: absolute;
  bottom: 0;
  background-color: #e4e4e4;
  border-radius: 15px;
  width: 300px;
  height: 500px;
  overflow: auto;
  margin-left: 20px;
}
.card::-webkit-scrollbar {
  width: 12px;
  height: 150px;
}

.card::-webkit-scrollbar-track {
  background: #e4e4e4;
}

.card::-webkit-scrollbar-thumb {
  background-color: #dddada;
  border-radius: 20px;
}
.card::-webkit-scrollbar-thumb:hover {
  background-color: #2196f3;
}

.btn-pill {
  border-radius: 20px;
  padding: 5px 20px 5px 20px;
}

.arrow {
  position: fixed;
  margin-left: 105px;
  margin-top: -40px;
}

.title {
  color: white;
  background-color: #2196f3;
  margin-bottom: -8px;
}

.content {
  background-color: white;
}

.container-fluid {
  height: 2000px;
}
</style>
