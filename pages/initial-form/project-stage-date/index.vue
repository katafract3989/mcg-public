<template>
  <div class="content-area">
    <ProgressBar :step="3" />
    <div class="content-area__workspace">
      <ProjectStageDate />
    </div>
  </div>
</template>
<script>
export default {
  components: {
    ProjectStageDate: () =>
      import('~/components/Pages/InitialForm/ProjectStageDate'),
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
  min-height: 100%;
  display: flex;

  &__workspace {
    margin-left: 527px;
    min-height: 100%;
  }
}
</style>
