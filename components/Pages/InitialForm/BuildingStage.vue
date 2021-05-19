<template>
  <div class="w-100 initial-component">
    <div class="title-page">
      <span>Step 2</span>
      <h1>Building Stage</h1>
    </div>
    <div class="content-page">
      <Card
        v-for="(type, i) in types"
        :key="i"
        :item="type"
        :selected-element="selected_element"
        :border="checkSelected(type.title)"
        @add-type="setData"
      />
    </div>
    <div class="d-flex justify-content-center">
      <NuxtLink class="initial-link-button" to="/initial-form/building-type"
        ><SvgIcon name="arrow2" class="mr-2" />BACK</NuxtLink
      >
      <NuxtLink class="initial-button" to="/initial-form/project-stage-date"
        >NEXT STEP</NuxtLink
      >
    </div>
  </div>
</template>
<script>
export default {
  components: {
    Card: () => import('~/components/Pages/InitialForm/components/Card'),
  },
  data() {
    return {
      types: [
        // {
        //   title: 'I own the property',
        //   icon: 'house',
        // },
        // {
        //   title: 'I am in contractor for the property',
        //   icon: 'Group 146',
        // },
        // {
        //   title: 'I am thinking of purchasing, a property',
        //   icon: 'Group',
        // },
        // {
        //   title: 'Other',
        //   icon: 'Group 117',
        // },
      ],
      selected_element: 'stage',
    }
  },
  mounted() {
    this.$axios
      .get(
        `${process.env.API_DOMAIN}/api/v1/references/requests/buildingStages`
      )
      .then((response) => (this.types = response.data.data.building_stages))
  },
  methods: {
    checkSelected(index = null) {
      if (index === this.$store.getters['initialForm/getData'].building_stage) {
        return true
      }
    },
    setData(stage) {
      this.$store.dispatch('initialForm/addBuildingStage', stage)
    },
  },
}
</script>
<style lang="scss" scoped>
h1,
h2 {
  text-transform: uppercase;
}
.title-page {
  margin-top: 85px;
  text-align: center;

  span {
    color: #979898;
  }
}
.content-page {
  margin-top: 50px;
  left: 257px;
  min-height: 100%;
  display: flex;
  justify-content: center;
  width: 100%;
  margin-bottom: 180px;
}
</style>
