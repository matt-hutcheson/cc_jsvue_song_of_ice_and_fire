<template lang='html'>
  <article>
    <h2>Characters Loyal to {{selectedHouse.name}}</h2>
    <ul>
      <li v-for="(character,index) in characters" v-if="character.name" v-on:click='handleClick(character)' :key="index">
        {{character.name}} {{character.id}}
      </li>
    </ul>
  </article>
</template>

<script>
import {eventBus} from '../main.js'
export default {
    name: 'characters-list',
    props: ['characters', 'selectedHouse'],
    methods: {
      handleClick: function (character) {
        eventBus.$emit('character-selected', character)
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