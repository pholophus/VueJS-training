<template>
    <div class="about flex flex-col items-center">
      <div class=" absolute inset-0 z-0" @click="modal = flase"></div>
        <input type="text" class="bg-gray-300 px-4 py-2 z-10" autocomplete="off" v-model="state" @focus="modal = true">
        <div v-if="filterStates && modal" class="z-10">
            <ul class="w-48 bg-gray-800 text-white ">
                <li v-for="filteredState in filteredStates" :key="filteredState.id" class="py-2 border-b cursor-pointer" @click="setState(filteredState)">{{filteredState}}</li>
            </ul>
        </div>

        <ul>
            <li v-for="stated in states" :key="stated">{{stated}}</li>
        </ul>

    </div>
</template>

<script>
const axios = require('axios');

export default {
    data: function() {
        return {
            state: '',
            modal: false,
            states: //['selangor', 'sarawak', 'sabah', 'sandakan', 'perlis', 'pahang'],
            [],
            filteredStates: []
        }
    },

    mounted: function() {

    axios.get('https://jsonplaceholder.typicode.com/posts')
    .then(response => this.states.push(response.title))
    //need to be wraped in array because posts return array of posts
    //.catch(error => this.state = [{title: 'No posts found'}])
    .finally(() => console.log('Data finished rendered'));
      
    this.filterStates();
    },

    methods: {
        filterStates() {
            if( this.state.length == 0) {
              this.filteredStates = this.state;
            }

            this.filteredStates = this.states.filter(state => {
                return state.toLowerCase().startsWith(this.state.toLowerCase());
            })
        },
        setState(state) {
            this.state = state;
            this.modal = false;
        },

        showStates() {
            return this.states;
        }
    },

    watch: {
      state() {
        this.filterStates();
      }
    }
}
</script>