<template lang='html'>
  <nav>
      <house-arryn :houseArryn='houseArryn'></house-arryn>
  </nav>
</template>

<script>
import houseArryn from './greatHouses/houseArryn.vue';

export default {
    data () {
        return {
            houseArryn: null,
            houseBaratheon: null,
            houseGreyjoy: null,
            houseLanister: null,
            houseMartell: null,
            houseStark: null,
            houseTully: null
        }
    },
    props: ['greatHouses'],
    components: {
        'house-arryn': houseArryn
    }

}
</script>

<style lang='css' scoped>

</style>