<template>
  <div class="content-area">
    <ProgressBar :step="6" :final="final" />
    <div class="content-area__workspace">
      <client-only placeholder="Loading...">
        <Final v-if="!final" @final-slide="finalSlide" />
        <Congratulations v-else />
      </client-only>
    </div>
  </div>
</template>
<script>
export default {
  components: {
    Final: () => import('~/components/Pages/InitialForm/Final'),
    Congratulations: () =>
      import('~/components/Pages/InitialForm/Сongratulations'),
    ProgressBar: () => import('~/components/Pages/InitialForm/ProgressBar'),
  },
  data() {
    return { final: false }
  },
  layout: 'empty',
  mounted() {
    this.final = this.$store.getters['initialForm/getData'].completed
  },
  methods: {
    finalSlide() {
      this.final = true
      this.$store.dispatch('initialForm/completeForm')
    },
  },
}
</script>

<style lang="scss" scoped>
.content-area {
  display: flex;
  flex-direction: column;
}
</style>
