<template>
    <div class="info-row">
        <span class="info-row--text">
            {{ text }}
        </span>
        <span class="info-row--slot">
            <slot></slot>
        </span>
    </div>
</template>

<script>
export default {
  name: 'InfoRow',
  props: {
    text: String
  }
}
</script>

<style scoped>
  .info-row{
      display: flex;
      justify-content: space-between;
      margin: 0;
      margin-bottom: 4px;
      padding-left: 16px;
      padding-right: 14px;
      padding-top: 14px;
      padding-bottom: 4px;
      background-color: #fff;
  }
  .info-row--text{
      line-height: 14px;
  }

  .info-row--slot{
      height: 35px;
      width: 100px;
  }
</style>
