<template>
    <section>
        <div v-if="selectedGreatHouse.id === 7" class="arran-banner"></div>
        <div v-if="selectedGreatHouse.id === 15" class="baratheon-banner"></div>
        <div v-if="selectedGreatHouse.id === 169" class="greyjoy-banner"></div>
        <div v-if="selectedGreatHouse.id === 229" class="lannister-banner"></div>
        <div v-if="selectedGreatHouse.id === 285" class="martell-banner"></div>
        <div v-if="selectedGreatHouse.id === 362" class="stark-banner"></div>
        <div v-if="selectedGreatHouse.id === 395" class="tully-banner"></div>
        <div v-if="selectedGreatHouse.id === 398" class="tyrell-banner"></div>
    </section>
</template>

<script>
export default {
    name: 'banners',
    props: ['selectedGreatHouse']
}
</script>

<style scoped>

section{
    height: 100%;
}

.arran-banner {
    height: 100%;
    background: url('../assets/images/banners/arran_banner.png') no-repeat center right;
    background-size: contain;
}

.baratheon-banner {
    height: 100%;
    background: url('../assets/images/banners/baratheon_banner.png') no-repeat center right;
    background-size: contain;
}

.greyjoy-banner {
    height: 100%;
    background: url('../assets/images/banners/greyjoy_banner.png') no-repeat center right;
    background-size: contain;
}

.lannister-banner {
    height: 100%;
    background: url('../assets/images/banners/lannister_banner.png') no-repeat center right;
    background-size: contain;
}

.martell-banner {
    height: 100%;
    background: url('../assets/images/banners/martell_banner.png') no-repeat center right;
    background-size: contain;
}

.stark-banner {
    height: 100%;
    background: url('../assets/images/banners/stark_banner.png') no-repeat center right;
    background-size: contain;
}

.tully-banner {
    height: 100%;
    background: url('../assets/images/banners/tully_banner.png') no-repeat center right;
    background-size: contain;
}

.tyrell-banner {
    height: 100%;
    background: url('../assets/images/banners/tyrell_banner.png') no-repeat center right;
    background-size: contain;
}

</style>