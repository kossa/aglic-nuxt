<template>
  <div>
    <label>Wilayas</label>
    <!-- <select name="" id="">
      <option value="" v-for="w in wilayas" :key="w.id">{{w.name}}</option>
    </select> -->
    {{ wilaya_id }}
    <v-select
      v-model="wilaya_id"
      :items="wilayas"
      label="Wilayas"
      item-value="id"
      item-text="name"
    ></v-select>

    <v-select
      :items="communes"
      label="Communes"
      item-value="id"
      item-text="name"
    ></v-select>
  </div>
</template>

<script>
export default {
  props: {
    wilayas: {
      type: Array,
      default: () => []
    }
  },

  data() {
    return {
      wilaya_id: null,
      communes: [],
    }
  },

  watch: {
    async wilaya_id() {
      this.$nextTick(() => {
        this.$nuxt.$loading.start()
      })
      const communes = await this.$axios.$get(`https://algerian-cities.bel4.com/api/wilayas/${this.wilaya_id}/communes`)

      this.communes = communes

      this.$toast.success('Wilayas loaded')

    }
  }

}
</script>

<style>

</style>
