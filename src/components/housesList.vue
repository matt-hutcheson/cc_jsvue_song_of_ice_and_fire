<template lang='html'>
  <article>
      <h2>Houses Loyal to {{selectedHouse.name}}</h2>
    <ul>
      <li v-for="(house,index) in houses" :key="index" v-on:click="handleClick(house)">
        {{house.name}} {{house.id}}
      </li>
    </ul>
  </article>
</template>

<script>
import {eventBus} from '../main.js'
export default {
    name: 'houses-list',
    props: ['houses', 'selectedHouse'],
    methods: {
        handleClick: function (house) {
        eventBus.$emit('house-selected', house)
        }
    }
}
</script>

<style lang='css' scoped>

li:hover {
    cursor: pointer;
    color: #fcbe32;
}

</style>