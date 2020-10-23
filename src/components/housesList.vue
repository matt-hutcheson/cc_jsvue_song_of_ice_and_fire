<template langg='html'>
  <article>
    <ul>
      <li v-for="(house,index) in houses" :key="index">
        {{house.name}} {{house.id}}
      </li>
    </ul>
  </article>
</template>

<script>
export default {
    props: ['houses']

}
</script>

<style lang='css' scoped>

</style>