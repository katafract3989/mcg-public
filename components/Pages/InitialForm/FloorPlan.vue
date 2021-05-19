<template>
  <div class="w-100 initial-component">
    <div class="title-page">
      <span>Step 4</span>
      <h1>Floor Plan</h1>
      <span style="font-size: 30px">Load a plan of your current building</span>
    </div>
    <div class="content-page">
      <AddFile class="mt-3" :variety="`floor-plan`" />
      <b-form-textarea
        id="textarea"
        v-model="data"
        class="mt-3"
        placeholder="Input something here if you have any information..."
        rows="8"
        @change="setInfo"
      ></b-form-textarea>
    </div>
    <div class="d-flex justify-content-center button-page">
      <NuxtLink
        class="initial-link-button"
        to="/initial-form/project-stage-date"
        ><SvgIcon name="arrow2" class="mr-2" />BACK</NuxtLink
      >
      <NuxtLink class="initial-button" to="/initial-form/rooms"
        >NEXT STEP</NuxtLink
      >
    </div>
  </div>
</template>
<script>
export default {
  components: {
    AddFile: () => import('~/components/Pages/InitialForm/components/AddFile'),
  },

  data() {
    return {
      data: '',
    }
  },

  watch: {
    room() {
      this.reqestStore()
    },
  },

  mounted() {
    this.reqestStore()
  },
  methods: {
    reqestStore() {
      this.data = this.$store.getters[
        'initialForm/getData'
      ].additional_info_floor_plan
    },
    setInfo() {
      this.$store.dispatch('initialForm/addAdditionalInfoFloorPlan', this.data)
    },
  },
}
</script>
<style lang="scss" scoped>
h1,
h2 {
  text-transform: uppercase;
  margin-bottom: 20px;
}
textarea {
  box-shadow: none;
  resize: none;
}
.title-page {
  margin-top: 85px;
  text-align: center;
}
.title-page span {
  color: #979898;
  margin-bottom: 10px;
  font-weight: 500;
  line-height: 140%;
}
.content-page {
  margin: 35px auto;
  left: 257px;
  min-height: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  width: 610px;
  margin-bottom: 50px;
}
</style>
