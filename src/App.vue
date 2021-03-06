<template>
  <div id="app">
    <header class="header">
      <Input :placeholder="placeholder" @writeText="onInputText"></Input>
      <Spinner :isRunning="showSpinner" />
    </header>
    <main class="main">
      <InfoRow  v-for="(row, ind) in rows" :key="row.text" :text="row.text">
        <Button @click="onAdd(ind)" :text="rowBtn" bgColor="#40B159"></Button>
      </InfoRow>
      <div class="added-list" v-if="savedRows.length">
        <hr>
        <hr>
        <p class="added-list--head">
          {{ staticText.main.listAdded }}
        </p>
        <InfoRow  v-for="row in savedRows" :key="row.text" :text="row.text">
        </InfoRow>
      </div>
    </main>
    <footer class="footer">
      <Button @click="toggleSearch" bgColor="#7382CD" :text="footerBtnText"></Button>
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
      rows: [],
      savedRows: [],
      textToSearch: ''
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
  },
  methods: {
    onInputText(text){
      this.textToSearch = text;
      if( this.autoSearchEnabled ){
        this.getDataFromApi(text);
      } 
    },
    async getDataFromApi(query){
      if(query.length < 2 ) return;
      this.showSpinner = true;
      try{
        const data = await fetch(config.API_URL, {
          method: 'POST',
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json',
            'Authorization': `Token ${config.API_TOKEN}`
          },
          mode: 'cors',
          body: JSON.stringify({ query })
        }).then( res => res.json() );
        this.rows = data.suggestions.map( i => ({text: i.value}) )
      } catch(e){
        console.log(e);
        alert(this.staticText.alerts.onFetchError);
      } finally{
        this.showSpinner = false;
      }
    },
    onAdd(ind){
      const candidate = this.rows[ind];
      if( !this.savedRows.includes(candidate) )
        this.savedRows.push( candidate );
    },
    toggleSearch(){
      this.autoSearchEnabled = !this.autoSearchEnabled;
    }
  },
  watch: {
    autoSearchEnabled(){
      if( this.autoSearchEnabled )
        this.getDataFromApi( this.textToSearch )
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
    padding-bottom: 50px;
  }
  #app{
    width: 100%;
    min-height: 100vh;
    display: grid;
    grid-template-rows: 53px 1fr;
  }
  .header{
    position: relative;
    z-index: 1;
  }
  .header input{
    width: 100%;
    padding-right: 45px;
    z-index: 2;
  }
  .header .spinner-container{
    position: absolute;
    right: 0;
    top: 0;
    z-index: 3;
  }
  .added-list--head{
    padding-left: 16px;
  }
  .main{
    padding-top: 24px;
    padding-bottom: 16px;
    background-color: #C4C4C4;
  }
  .footer{
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 64px;
  }
</style>
