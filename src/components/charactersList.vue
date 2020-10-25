<template lang='html'>
  <article>
    <h2>Characters Loyal to {{selectedHouse.name}}</h2>
    <ul>
      <li v-for="(character,index) in characters" v-if="character.name" :key="index">
        {{character.name}} {{character.id}}
      </li>
    </ul>
  </article>
</template>

<script>
export default {
    name: 'characters-list',
    props: ['characters', 'selectedHouse']
}
</script>

<style lang='css' scoped>

li:hover {
  cursor: pointer;
  color: #fcbe32;
}

</style>