<template>
  <div class="spinner-container">
    <div class="spinner" v-if="isRunning"></div>
  </div>
</template>

<script>
export default {
  name: 'Spinner',
  props: {
    isRunning: Boolean
  }
}
</script>

<style scoped>
  .spinner-container{
      height: 100%;
      display: flex;
  }
  .spinner{
      margin: auto;
      background: url('../assets/spinning-loading.gif');
      background-size: 300%;
      background-position: center;
      background-repeat: no-repeat;
      width: 40px;
      height: 40px;
  }
</style>