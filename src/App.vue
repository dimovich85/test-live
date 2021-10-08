<template>
  <div id="app">
    <header class="header">
      <Input :placeholder="placeholder"></Input>
      <Spinner :isRunning="showSpinner" />
    </header>
    <main class="main">
      <InfoRow v-for="row in rows" :key="row.text" :text="row.text">
        <Button :text="rowBtn" bgColor="#40B159"></Button>
      </InfoRow>
    </main>
    <footer class="footer">
      <Button bgColor="#7382CD" :text="footerBtnText"></Button>
    </footer>
  </div>
</template>

<script>
import Input from '@/components/input.vue'
import Spinner from '@/components/spinner.vue'
import InfoRow from '@/components/info-row.vue'
import Button from '@/components/button.vue'
import strRes from '@/resources/lang'
import config from '@/configs/config'


export default {
  name: 'App',
  components: {
    Input,
    Button,
    Spinner,
    InfoRow
  },
  data(){
    const staticText = strRes(config.DEFAULT_LANG);
    return {
      staticText,
      autoSearchEnabled: true,
      showSpinner: false,
      rows: []
    }
  },
  computed: {
    placeholder(){
      return this.staticText.header.input.placeholder;
    },
    rowBtn(){
      return this.staticText.main.addBtn;
    },
    footerBtnText(){
      const slug = this.autoSearchEnabled ? 'onEnabled' : 'onDisabled';
      return this.staticText.footer.button[slug];
    }
  }
}
</script>

<style>
  *{
    box-sizing: border-box;
  }
  body{
    margin: 0;
    padding: 0;
    min-height: 100vh;
    font-family: 'Roboto', sans-serif;
    font-weight: 400;
  }
  #app{
    width: 100%;
    min-height: 100vh;
    display: grid;
    grid-template-rows: 53px 1fr 64px;
  }
  .header{
    display: flex;
    justify-content: space-between;
  }
  .main{
    padding-top: 24px;
    padding-bottom: 16px;
    background-color: #C4C4C4;
  }
</style>
