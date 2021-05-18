<template>
    <div class="breed-information" v-if="Object.keys(selectedBreed).length > 0">
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
            <v-btn
                color="orange lighten-2"
                text
            >
                More of this breed
            </v-btn>

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
</template>

<style lang="scss">
    .breed-information {
        width:100%;
        display:flex;
        flex-direction: column;
        align-items: center;
    }
</style>

<script>
export default {
    name:'breed-information',
    props:{
        selectedBreed:{
            type:Object,
            default:{}
        }
    },
    data(){
        return{
            show:false,
        }
    }
}
</script>
