<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';


export default {
  name: "App",
  components:{
    AppHeader,
    AppMain
  },
  data() {
        return {
            card: [],
            choose: 'Alien',
            link: ''
        }
  },
  created() {
    this.link = "https://db.ygoprodeck.com/api/v7/cardinfo.php"
        axios
            .get(this.link)
            .then((response) => {
                this.card = response.data.data.slice(0,24)
                
            });
  },
}

</script>

<template>

  <AppHeader/>
  <AppMain :cardList="card"/>

</template>

<style lang="scss">
@import './styles/main.scss'
</style>
