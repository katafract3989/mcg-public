<template>
  <div class="content-area">
    <ProgressBar :step="2" />
    <div class="content-area__workspace">
      <BuildingStage />
    </div>
  </div>
</template>
<script>
export default {
  components: {
    BuildingStage: () => import('~/components/Pages/InitialForm/BuildingStage'),
    ProgressBar: () => import('~/components/Pages/InitialForm/ProgressBar'),
  },
  data() {
    return {}
  },
  layout: 'empty',
  methods: {},
}
</script>

<style lang="scss" scoped>
.content-area {
  display: flex;
  flex-direction: column;
  min-height: 100%;

  &__workspace {
    margin-left: 25%;
    min-height: 100%;
  }
}
</style>
