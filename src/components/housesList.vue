<template lang='html'>
  <article>
      <h2>Houses Loyal to {{selectedHouse.name}}</h2>
    <ul>
      <li v-for="(house,index) in houses" :key="index">
        {{house.name}} {{house.id}}
      </li>
    </ul>
  </article>
</template>

<script>
export default {
    name: 'houses-list',
    props: ['houses', 'selectedHouse']

}
</script>

<style lang='css' scoped>

</style>