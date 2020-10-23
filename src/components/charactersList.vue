<template lang='html'>
  <article>
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
    props: ['characters']
}
</script>

<style lang='css' scoped>

</style>