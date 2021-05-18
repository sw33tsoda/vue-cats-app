<template>
    <div class="breed-information" v-if="Object.keys(selectedBreed).length > 0">
        <div class="split">
            <v-card
            class="mx-auto"
            max-width="344"
        >
            <v-img
                v-bind:src="selectedBreed.image.url"
                height="200px"
            ></v-img>

            <v-card-title>
                {{selectedBreed.name}}
            </v-card-title>

            <v-card-subtitle>
                {{selectedBreed.temperament}}
            </v-card-subtitle>

            <v-simple-table>
                <template v-slot:default>
                <thead>
                    <tr>
                    <th class="text-left">
                        Features
                    </th>
                    <th class="text-left">
                        Stats
                    </th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Origin</td>
                        <td>{{selectedBreed.origin}}</td>
                    </tr>
                    <tr>
                        <td>Weight</td>
                        <td>{{selectedBreed.weight.metric}} kilograms</td>
                    </tr>
                    <tr>
                        <td>Life span</td>
                        <td>{{selectedBreed.life_span}} years</td>
                    </tr>
                </tbody>
                </template>
            </v-simple-table>

            <v-card-actions>
            <!-- <v-btn
                color="orange lighten-2"
                @click="getCatsByBreed"
                text
            >
                More of this breed
            </v-btn> -->

            <v-spacer></v-spacer>

            <v-btn
                icon
                @click="show = !show"
            >
                <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
            </v-btn>
            </v-card-actions>

            <v-expand-transition>
            <div v-show="show">
                <v-divider></v-divider>

                <v-card-text>
                    {{selectedBreed.description}}
                </v-card-text>
            </div>
            </v-expand-transition>
        </v-card>
        </div>
        <div class="split">
            <v-row v-if="sameBreedCats.length > 0">
                <v-col
                v-for="(cat,index) of sameBreedCats"
                :key="index"
                class="d-flex child-flex"
                cols="4"
                >
                <v-img
                    :src="`${cat.url}`"
                    aspect-ratio="1"
                    class="grey lighten-2 rounded"
                    @click="viewFullSize(cat.url)"
                >
                    <template v-slot:placeholder>
                    <v-row
                        class="fill-height ma-0"
                        align="center"
                        justify="center"
                    >
                        <v-progress-circular
                        indeterminate
                        color="grey lighten-5"
                        ></v-progress-circular>
                    </v-row>
                    </template>
                </v-img>
                </v-col>
            </v-row>
        </div>
    </div>
</template>

<style lang="scss">
    .breed-information {
        width:100%;
        display:flex;
        flex-direction: row;
        justify-content: center;
        column-gap: 10px;
    }
</style>

<script>
import axios from 'axios'
export default {
    name:'breed-information',
    props:{
        selectedBreed:{
            type:Object,
            default:{}
        },
    },
    data(){
        return{
            show:false,
            sameBreedCats:[],
        }
    },
    methods:{
        getCatsByBreed:async function(){
            const apiResponse = await axios.get(`https://api.thecatapi.com/v1/images/search?breed_id=${this.selectedBreed.id}&limit=10`);
            this.sameBreedCats = [...apiResponse.data];
        },
        viewFullSize(url){
            window.open(url,'_blank');
        }
    },
    watch:{
        selectedBreed:function(newProps,oldProps){
            if (newProps.id !== oldProps.id) {
                this.getCatsByBreed();
            }
        },
    },
}
</script>
