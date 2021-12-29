<template>
  <div>
    <h1>Wilayas</h1>
    <WilayaCommune :wilayas="wilayas" />
  </div>
</template>

<script>
import WilayaCommune from '~/components/WilayaCommune.vue'

export default {
  components: {
    WilayaCommune,
  },

  data() {
    return {
    }
  },

  async asyncData({$axios}) {
    const wilayas = await $axios.$get('https://algerian-cities.bel4.com/api/wilayas')

    return { wilayas }
  },
}
</script>

<style></style>
