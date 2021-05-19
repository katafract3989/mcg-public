<template>
  <div class="component initial-component w-100">
    <div class="component__header">
      <HeaderComponent :number="2" :title="`Parts to renovation`" />
    </div>
    <div
      v-dragscroll
      class="component__settings"
      :style="`height: ${selected.length >= 1 ? '300px' : '0px'}`"
    >
      <div
        v-for="(work, i) in selected"
        :key="i"
        class="component__settings__part d-flex justify-content-between"
      >
        <div class="component__settings__part-title">
          <img
            :src="`/static/images/icon-works/${work.icon}.svg`"
            alt=""
            class="mr-4"
          />
          <span>{{ work.title }}</span>
        </div>

        <div class="d-flex component__settings__part-action">
          <multiselect
            v-model="work.action"
            :options="actions"
            track-by="id"
            label="title"
            select-label=""
            :searchable="false"
            selected-label=""
            deselect-label=""
            placeholder="Select"
            class="initial-multiselect"
          >
            <template slot="singleLabel" slot-scope="props"
              ><span class="option__title">
                <SvgIcon :name="props.option.icon" />{{ props.option.title }}
              </span></template
            >
            <template slot="option" slot-scope="props"
              ><SvgIcon :name="props.option.icon" />
              <div class="option__desc">
                {{ props.option.title }}
              </div>
            </template>
          </multiselect>
          <SvgIcon
            name="close"
            class="little-icon"
            style="color: red"
            @click="selected.splice(i, 1)"
          />
        </div>
      </div>
    </div>
    <div class="component__renovation__add-work" @click="addWork">
      <div class="component__renovation__add-work-icon">+</div>
      Add Parts of renovation
    </div>
    <AddWork :id="room.id" :list="selected" @save-works="saveWorks" />
  </div>
</template>
<script>
import _ from 'lodash'
export default {
  components: {
    AddWork: () => import('~/components/Modals/InitialForm/AddWork'),
    HeaderComponent: () =>
      import('~/components/Pages/InitialForm/components/HeaderComponent'),
  },
  props: {
    room: {
      type: Object,
      required: false,
      default: () => {},
    },
  },
  data() {
    return {
      actions: [],
      selected: [],
      data: {},
    }
  },
  watch: {
    room() {
      this.requestStore()
    },
    selected() {
      this.updateSelected()
    },
  },
  mounted() {
    this.$axios
      .get(`${process.env.API_DOMAIN}/api/v1/references/requests/workActions`)
      .then((response) => (this.actions = response.data.data.work_actions))
    this.requestStore()
  },
  methods: {
    addWork() {
      this.$bvModal.show('add-work')
    },
    saveWorks(works) {
      this.selected = _.cloneDeep(works)
      this.$bvModal.hide('add-work')
    },
    updateSelected() {
      this.data.works = _.cloneDeep(this.selected)
      this.data.id_room = this.room.index
      this.$store.dispatch('initialForm/addWorks', this.data)
    },
    requestStore() {
      this.selected =
        this.room.works !== undefined ? _.cloneDeep(this.room.works) : []
    },
  },
}
</script>
<style lang="scss" scoped>
.component {
  &__settings {
    margin-top: 10px;
    display: flex;
    flex-direction: column;
    max-height: 50vh;
    overflow: auto;

    &__part {
      display: flex;
      margin-top: 10px;
      justify-content: space-between;
      justify-content: center;
      align-items: center;
      min-height: 65px !important;
      border: 1px solid #d4d4d4;
      font-size: 18px;
      width: 99%;

      &-title {
        margin-left: 30px;

        svg {
          color: #0085ff;
          margin-right: 10px;
        }
      }

      &-action {
        display: flex;
        align-items: center;
        color: #979898;
        margin-right: 30px;

        svg {
          margin-right: 10px;
          color: #0085ff;
          margin-left: 10px;
          cursor: pointer;
        }

        span {
          font-size: 18px;
          display: flex;
          align-items: center;
          text-align: right;
          color: #0085ff;
        }
      }
    }
  }
  &__renovation {
    &__add-work {
      color: #0085ff;
      margin-top: 10px;
      font-family: 'Lato';
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 65px !important;
      background: #f7f9fc;
      border: 1px dashed #aad5fc;
      box-sizing: border-box;
      cursor: pointer;
      width: 99%;
      &-icon {
        width: 26px;
        height: 26px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 19px;
        background: #eef4fd;
        border-radius: 8px;
        margin-right: 10px;
      }
    }
  }
}
</style>
