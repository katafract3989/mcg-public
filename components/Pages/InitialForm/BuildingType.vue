<template>
  <div class="initial-component">
    <div class="title-page">
      <span>Step 1</span>
      <h1>Building type</h1>
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
      <NuxtLink class="initial-link-button" to="/initial-form"
        ><SvgIcon name="arrow2" class="mr-2" />BACK</NuxtLink
      >
      <NuxtLink class="initial-button" to="/initial-form/building-stage"
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
        //   title: 'Single/Multi-family home',
        //   icon: 'house',
        // },
        // {
        //   title: 'Apartment building',
        //   icon: 'Group 117',
        // },
      ],
      selected_element: 'type',
    }
  },
  mounted() {
    this.$axios
      .get(`${process.env.API_DOMAIN}/api/v1/references/requests/buildingTypes`)
      .then((response) => (this.types = response.data.data.building_types))
  },
  methods: {
    checkSelected(index = null) {
      if (index === this.$store.getters['initialForm/getData'].building_type) {
        return true
      }
    },
    setData(type) {
      this.$store.dispatch('initialForm/addBuildingType', type)
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
  display: flex;
  justify-content: center;
  width: 100%;
  margin-bottom: 10%;
}
</style>
