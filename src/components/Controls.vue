<template>
  <div class="controls" v-if="breedsList.length > 0">
      <v-select
          :items="breedsList"
          label="Select something"
          item-text="name"
          v-model="selected"
          return-object
          solo
        ></v-select>
  </div>
</template>

<style lang="scss">
    .controls {
        padding-top: 50px;
        width: 100%;
        display:flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
    }
</style>

<script>
import Axios from 'axios';
export default {
    name:'controls',
    data(){
        return{
            selected:{},
            breedsList:[],
        }
    },
    filters:{
        prepareSelectList:function(list){
            return list.map(value => value.name);
        }
    },
    methods:{
        getBreedsList:async function(){
            try {
                const apiResponse = await Axios.get('https://api.thecatapi.com/v1/breeds');
                this.breedsList = apiResponse.data;
            } catch (error) {
                console.log(error);
            }
        },
    },

    created() {
        this.getBreedsList();
    },
    updated() {
        console.log(this.selected);
        this.$emit('setSelectBreed',this.selected);
    }
}
</script>
