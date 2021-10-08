<template>
  <input type="text" :placeholder="placeholder">
</template>

<script>
export default {
  name: 'Input',
  props: {
    placeholder: String,
    value: String,
    type: String
  }
}
</script>

<style scoped>
  input{
    display: block;
    width: 100%;
    height: 100%;
    padding-top: 14px;
    padding-bottom: 14px;
    padding-left: 16px;
    padding-right: 16px;
    border: none;
  }
  input:focus{
    outline: none;
    box-shadow: 0 1px 2px 2px rgba(0,0,0,0.3);
  }
</style>
