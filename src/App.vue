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
            card: []
        }
  },  
  created() {
        axios
            .get('https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=Alien')
            .then((response) => {
                this.card = response.data.data.slice(0,20)
                
            });
    }
}

</script>

<template>

  <AppHeader/>
  <AppMain :cardList="card"/>

</template>

<style lang="scss">
@import './styles/main.scss'
</style>
