<template>
  <div class="initial-component">
    <div class="title-page">
      <span>Step 3</span>
      <h1>Project Stage Date</h1>
    </div>
    <div class="content__page">
      <div class="content__page-stage-item">
        <StageDate
          v-for="(item, i) in term"
          :key="i"
          :item="item"
          :border="checkSelected(item.title)"
          @add-stage-date="setData"
        />
      </div>
      <img
        :src="`/static/images/icon/101441.png`"
        width="753"
        height="471"
        alt=""
      />
    </div>
    <div class="d-flex justify-content-center">
      <NuxtLink class="initial-link-button" to="/initial-form/building-stage"
        ><SvgIcon name="arrow2" class="mr-2" />BACK</NuxtLink
      >
      <NuxtLink class="initial-button" to="/initial-form/floor-plan"
        >NEXT STEP</NuxtLink
      >
    </div>
  </div>
</template>
<script>
export default {
  components: {
    StageDate: () =>
      import('~/components/Pages/InitialForm/components/StageDate'),
  },
  data() {
    return {
      term: [
        {
          title: 'As soon as possible',
        },
        {
          title: 'In 1 month',
        },
        {
          title: 'In 2 month',
        },
        {
          title: 'In 3-6 month',
        },
        {
          title: 'Not shure',
        },
      ],
    }
  },
  mounted() {
    this.$axios
      .get(
        `${process.env.API_DOMAIN}/api/v1/references/requests/projectStateDates`
      )
      .then((response) => (this.term = response.data.data.project_stage_dates))
  },
  methods: {
    checkSelected(index = null) {
      if (
        index === this.$store.getters['initialForm/getData'].project_stage_date
      ) {
        return true
      }
    },
    setData(date) {
      this.$store.dispatch('initialForm/addProjectStageDate', date)
    },
  },
}
</script>
<style lang="scss">
h1,
h2 {
  text-transform: uppercase;
}
@media (max-width: 1400px) {
  img {
    display: none;
  }
}
.title-page {
  margin-top: 85px;
  text-align: center;

  span {
    font-size: #979898;
  }
}
.content__page {
  margin-top: 50px;
  display: flex;
  max-height: 500px;
  overflow: auto;

  &-stage-item {
    flex-direction: column;
    margin-left: 60px;
  }
}
</style>
