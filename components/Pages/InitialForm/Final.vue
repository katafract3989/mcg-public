<template>
  <div class="initial-component w-70" style="margin-left: 25%">
    <div class="title-page">
      <span>Step 6</span>
      <h1>Final</h1>
    </div>
    <div class="content-page">
      <div class="content-page__personal-data">
        <HeaderComponent :number="1" :title="`Personal data`" />
        <div class="content-page__fields">
          <div class="form-group">
            <div class="row mt-3">
              <div class="col-6 col-lg-6">
                <label>Name</label>
                <div class="initial-input-container">
                  <SvgIcon name="name" />
                  <input
                    v-model="form.personal.name"
                    type="text"
                    class="initial-input-form"
                    placeholder="Enter First Name"
                  />
                </div>
              </div>
              <div class="col-6 col-lg-6">
                <label>Last Name</label>
                <div class="initial-input-container">
                  <SvgIcon name="name" />
                  <input
                    v-model="form.personal.last_name"
                    type="text"
                    class="initial-input-form"
                    placeholder="Enter Last Name"
                  />
                </div>
              </div>
            </div>
            <div class="row mt-3">
              <div class="col-6 col-lg-6">
                <label>E-mail</label>
                <div class="initial-input-container">
                  <SvgIcon name="mail" />
                  <input
                    v-model="form.personal.email"
                    type="email"
                    :class="`initial-input-form ${
                      validation.email ? `is-invalid` : ``
                    }`"
                    placeholder="email@example.com"
                  />
                </div>
                <div class="invalid-feedback">
                  <div
                    v-for="(error, i) in validation.email"
                    :key="`errors-email-${i}`"
                  >
                    {{ error }}
                  </div>
                </div>
              </div>
              <div class="col-6 col-lg-6">
                <label>Phone</label>
                <div class="initial-input-container">
                  <SvgIcon name="phone" />
                  <masked-input
                    v-model="form.personal.phone"
                    :guide="false"
                    placeholder-char="#"
                    :mask="[
                      '+',
                      '1',
                      ' ',
                      '(',
                      /[1-9]/,
                      /\d/,
                      /\d/,
                      ')',
                      ' ',
                      /\d/,
                      /\d/,
                      /\d/,
                      '-',
                      /\d/,
                      /\d/,
                      /\d/,
                      /\d/,
                    ]"
                    type="text"
                    class="initial-input-form"
                    placeholder="+1 (___) ___-__-__"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <hr />
      <div class="content-page__address">
        <HeaderComponent :number="2" :title="`Address`" />
        <div class="content-page__fields">
          <div class="form-group">
            <div class="row mt-3">
              <div class="col-6 col-lg-6">
                <label>Address</label>
                <div class="initial-input-container">
                  <input
                    v-model="form.address.address"
                    type="text"
                    class="initial-input-form"
                    placeholder="Enter Address"
                    style="border: none"
                  />
                </div>
              </div>
              <div class="col-6 col-lg-6">
                <label>Street</label>
                <div class="initial-input-container">
                  <input
                    v-model="form.address.street"
                    type="text"
                    class="initial-input-form"
                    placeholder="Enter Street"
                    style="border: none"
                  />
                </div>
              </div>
            </div>
            <div class="row mt-3">
              <div class="col-6 col-lg-6">
                <div class="form-group">
                  <label>State</label>
                  <div class="initial-input-container">
                    <input
                      v-model="form.address.state"
                      type="text"
                      class="initial-input-form"
                      disabled
                      style="border: none"
                    />
                  </div>
                </div>
              </div>
              <div class="col-6 col-lg-6">
                <div class="form-group">
                  <label>City</label>
                  <div class="initial-input-container">
                    <input
                      v-model="form.address.city"
                      type="text"
                      class="initial-input-form"
                      style="border: none"
                      placeholder="Enter a City"
                    />
                  </div>
                </div>
              </div>
            </div>
            <div class="row">
              <div class="col-6 col-lg-6">
                <div class="form-group">
                  <label>Zip</label>
                  <div class="initial-input-container">
                    <input
                      v-model="form.address.zip"
                      type="text"
                      minlength="1"
                      maxlength="9"
                      class="initial-input-form"
                      style="border: none"
                      placeholder="Enter a zip"
                    />
                  </div>
                </div>
              </div>
              <div class="col-6 col-lg-6" style="margin-top: 35px">
                <div class="form-group">
                  <b-form-checkbox
                    v-model="form.personal.consent"
                    name="checkbox-3"
                    class="ml-3"
                    checked-value="true"
                    unchecked-value="false"
                  >
                    I consent to process personal data
                  </b-form-checkbox>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="d-flex justify-content-center mt-3">
        <NuxtLink class="initial-link-button" to="/initial-form/rooms"
          ><SvgIcon name="arrow2" class="mr-2" />BACK</NuxtLink
        >
        <div class="initial-button" @click="setData">Final</div>
      </div>
    </div>
  </div>
</template>
<script>
import states from '~/data/states'
export default {
  components: {
    HeaderComponent: () =>
      import('~/components/Pages/InitialForm/components/HeaderComponent'),
  },
  data() {
    return {
      form: {
        personal: {},
        address: {
          state: null,
        },
      },
      validation: {},
      states,
    }
  },
  mounted() {
    const data = this.$store.getters['initialForm/getData']
    this.form.address.state = data.state
    // this.form.address = data.address
    // this.form.personal = data.personal_data
  },
  methods: {
    setData() {
      this.$store.dispatch('initialForm/addPersonalData', this.form)
      this.$emit('final-slide', null)
    },
  },
}
</script>
<style lang="scss" scoped>
h1,
h2 {
  text-transform: uppercase;
}
.initial-input-container {
  border: 1px solid #dedede;
  display: flex;
  align-items: center;
  height: 44px;
  svg {
    margin: 8px;
    color: #979898;
  }
}
.initial-input-form {
  border: none;
  border-left: 1px solid #dedede;
  width: 100%;
  height: 38px;
  padding-left: 5px;
  outline: none;
  color: #979898;
}
.title-page {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 85px;

  span {
    color: #979898;
  }
}
.content-page {
  display: flex;
  padding-left: 76px;
  flex-direction: column;
}
</style>
