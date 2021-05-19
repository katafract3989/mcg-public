<template>
  <div>
    <div>
      <div>
        <Header />
        <Map @add-state="addState" />
      </div>
      <div class="d-flex justify-content-center">
        <NuxtLink class="initial-button" to="/initial-form/building-type"
          >NEXT STEP</NuxtLink
        >
      </div>
    </div>
    <Footer class="footer" :link="true" />
  </div>
</template>
<script>
export default {
  components: {
    Header: () => import('~/components/Pages/InitialForm/Header'),
    Map: () => import('~/components/Pages/InitialForm/Map'),
    Footer: () => import('~/components/Pages/InitialForm/Footer'),
  },
  data() {
    return {}
  },
  methods: {
    addState(state) {
      this.$store.dispatch('initialForm/addState', state)
    },
  },
}
</script>
