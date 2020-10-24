<template lang='html'>
    <section>
        <nav>
            <button v-for="(house, id) in greatHouses" :key="id" v-on:click="handleGreatHouseClick(house)">{{house.name}}</button>
        </nav>
    </section>
</template>

<script>
import houseArryn from './greatHouses/houseArryn.vue';
import {eventBus} from '../main.js';

export default {
    name: 'great-houses',
    data () {
        return {
            selectedGreatHouse: null
        }
    },
    props: ['greatHouses'],
    methods: {
        handleGreatHouseClick: function(house) {
            this.selectedGreatHouse = house
            eventBus.$emit('great-house-selected', this.selectedGreatHouse)
        }
    }
}
</script>

<style lang='css' scoped>
nav {
    display: flex;
    flex-flow: row;
    justify-content: space-around;
}

nav > button {
    padding: 10px;
    width: 35ch;
    background-color: #e1eef6;
    color: #004e66;
    font-family: "GoT", Helvetica, Arial;
    font-size: medium;
}

nav > button:hover {
    cursor: pointer;
    background-color: #fcbe32;
}

</style>