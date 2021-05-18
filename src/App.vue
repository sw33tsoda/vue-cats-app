<template>
  <div class="main" data-app>
    <controls v-on:setSelectBreed="handleSetSelectBreed"></controls>
    <breed-information v-bind:selectedBreed="selectedBreed"></breed-information>
  </div>
</template>

<style lang="scss">
  * {
    padding: 0;
    margin:0;
  }

  body {
    background: #9cecfb; /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #9cecfb, #65c7f7, #0052d4); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(to right, #9cecfb, #65c7f7, #0052d4); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
    background-attachment: fixed;

  }

  .main {
    width: 100%;
    height: 100vh;
    // background-color:silver;
  }
</style>

<script>
import BreedInformation from './components/BreedInformation.vue';
import Controls from './components/Controls.vue'
export default {
  components: { Controls, BreedInformation },
  name:'app',
  data(){
    return{
      selectedBreed:{},
    }
  },
  methods:{
    handleSetSelectBreed:function(payload){
      this.selectedBreed = payload;
    }
  }
}
</script>
