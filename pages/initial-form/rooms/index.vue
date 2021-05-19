<template>
  <div class="content-area">
    <ProgressBar :step="5" />
    <div class="content-area__workspace">
      <RoomSelector />
    </div>
  </div>
</template>
<script>
export default {
  components: {
    RoomSelector: () => import('~/components/Pages/InitialForm/RoomSelector'),
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
body {
  background: #fff;
}
.content-area {
  display: flex;
  flex-direction: column;

  &__workspace {
    margin-left: 25% !important;
  }
}
</style>
