<template>
    <button @click="emitClick" :style="styles"> {{ text }} </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    text: String,
    bgColor: String
  },
  computed: {
      styles(){
          return `background-color: ${this.bgColor};`;
      }
  },
  methods: {
    emitClick(e){
      this.$emit('click', e);
    }
  }
}
</script>

<style scoped>
  button{
      display: block;
      text-align: center;
      border: none;
      width: 100%;
      height: 100%;
      cursor: pointer;
  }
</style>
