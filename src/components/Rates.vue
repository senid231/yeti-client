<template>
<div id="rates">
  <h3>Rates</h3>
  <b-spinner variant="primary" label="Spinning" v-if="loading"/>
  <b-table hover :items="rates" v-if="rates"/>
</div>
</template>

<script>
export default {
  name: 'rates',
  data () {
    return {
    }
  },
  computed: {
    rates: function () {
      return this.$store.state.rates.rates.data
    },
    loading: function () {
      return this.$store.state.rates.requestPending
    }
  },
  methods: {
    getRates: function () {
      this.$store.dispatch('getRates')
        .catch(err => {
          this.$notify({
            type: 'error',
            title: err[0].title,
            text: err[0].detail
          })
        })
    }
  },
  created: function () {
    this.getRates()
  }
}
</script>