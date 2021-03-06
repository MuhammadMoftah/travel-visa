<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="5" class="pa-0">
      <v-card class="" flat>
        <h2 class="text-center py-5" style="font-weight: 900">دايركت فيزا</h2>

        <v-tabs
          v-model="tab"
          background-color="white"
          centered
          icons-and-text
          color="#FC840B"
        >
          <v-tabs-slider></v-tabs-slider>

          <v-tab href="#tab-1" class="font-weight-bold">
            تأشيرات
            <v-icon>mdi-passport</v-icon>
          </v-tab>

          <v-tab href="#tab-2" class="font-weight-bold">
            معاهد
            <v-icon>mdi-school</v-icon>
          </v-tab>

          <v-tab href="#tab-3" class="font-weight-bold" v-if="false">
            بكجات
            <v-icon>mdi-vector-circle</v-icon>
          </v-tab>
        </v-tabs>

        <v-tabs-items v-model="tab" style="min-height: 500px">
          <v-tab-item :value="'tab-1'">
            <v-card flat color="#F9F9F9">
              <v-card-text>
                <v-row class="pt-2 px-2">
                  <v-btn-toggle v-model="btns" dense tile color="#FC840B" group>
                    <v-btn
                      value="one"
                      class="group-btn font-weight-bold rounded-lg pb-1"
                    >
                      اتجاه واحد
                    </v-btn>

                    <v-btn
                      value="two"
                      class="group-btn font-weight-bold rounded-lg pb-1"
                    >
                      ذهاب واياب
                    </v-btn>

                    <v-btn
                      value="three"
                      class="group-btn font-weight-bold rounded-lg pb-1"
                    >
                      وجهات متعدده
                    </v-btn>
                  </v-btn-toggle>
                </v-row>
                <v-row class="mt-7 px-3">
                  <div
                    class="white pt-6 pb-0 travel-container px-4 rounded-lg shadow"
                    style="width: 100%"
                  >
                    <v-btn
                      text
                      fab
                      absolute
                      top
                      bottom
                      left
                      class="my-auto"
                      x-small
                      color="#FC840B"
                      @click="replace"
                    >
                      <v-icon>mdi-arrow-up-down</v-icon>
                    </v-btn>
                    <v-col cols="12" class="pa-0">
                      <v-text-field
                        label="من"
                        v-model="place1"
                        color="#FC840B"
                        id="place1"
                        class="mb-5"
                        dense
                        readonly
                        prepend-icon="mdi-moon-new"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" class="pa-0">
                      <v-text-field
                        dense
                        label="الي"
                        readonly
                        v-model="place2"
                        color="#FC840B"
                        prepend-icon="mdi-map-marker"
                      ></v-text-field>
                    </v-col>
                  </div>
                </v-row>

                <v-row justify="center" align="center">
                  <v-col cols="6" class="pb-0">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      :return-value.sync="date"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="date"
                          label="تاريخ المغادرة"
                          prepend-inner-icon="mdi-arrow-right"
                          readonly
                          dense
                          color="#FC840B"
                          filled
                          background-color="white"
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="date" no-title scrollable>
                        <v-spacer></v-spacer>
                        <v-btn text color="primary" @click="menu = false">
                          Cancel
                        </v-btn>
                        <v-btn
                          text
                          color="primary"
                          @click="$refs.menu.save(date)"
                        >
                          OK
                        </v-btn>
                      </v-date-picker>
                    </v-menu>
                  </v-col>

                  <v-col cols="6" class="pb-0">
                    <v-menu
                      ref="menu2"
                      v-model="menu2"
                      :close-on-content-click="false"
                      :return-value.sync="date"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="date2"
                          label="تاريخ العوده"
                          prepend-inner-icon="mdi-arrow-left"
                          readonly
                          dense
                          filled
                          background-color="white"
                          v-bind="attrs"
                          color="#FC840B"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="date2" no-title scrollable>
                        <v-spacer></v-spacer>
                        <v-btn text color="primary" @click="menu = false">
                          Cancel
                        </v-btn>
                        <v-btn
                          text
                          color="primary"
                          @click="$refs.menu2.save(date)"
                        >
                          OK
                        </v-btn>
                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <v-row class="mt-5 px-3" @click="sheet = !sheet">
                  <v-text-field
                    value="1 بالغ , درجة اقتصادية"
                    label="عدد الركاب والدراجات الاقتصادية"
                    prepend-inner-icon="mdi-seat-passenger"
                    readonly
                    dense
                    color="#FC840B"
                    filled
                    background-color="white"
                  ></v-text-field>
                </v-row>

                <v-row
                  justify="space-between"
                  class="pl-1 pr-4 mb-4 mt-6"
                  align="center"
                >
                  <p
                    class="ma-0"
                    style="cursor: pointer"
                    @click="check = !check"
                  >
                    اعرض الرحلات المباشرة فقط
                  </p>
                  <v-checkbox
                    color="#FC8004"
                    v-model="check"
                    class="pa-0 my-1"
                    hide-details
                  >
                  </v-checkbox>
                </v-row>

                <v-row justify="center" class="px-3" align="center">
                  <v-btn
                    block
                    color="#FC8004"
                    elevation="1"
                    dark
                    class="rounded-lg py-6"
                  >
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      width="18"
                      height="18"
                      fill="currentColor"
                      class="bi bi-search mx-2"
                      viewBox="0 0 16 16"
                    >
                      <path
                        d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"
                      />
                    </svg>
                    ابحث عن رحلات
                  </v-btn>
                </v-row>
              </v-card-text>
            </v-card>
          </v-tab-item>
          <v-tab-item :value="'tab-2'">
            <v-card flat>
              <v-card-text>{{ text }}</v-card-text>
            </v-card>
          </v-tab-item>
        </v-tabs-items>
      </v-card>
    </v-col>

    <v-bottom-sheet v-model="sheet">
      <v-sheet>
        <v-toolbar class="text-center" elevation="0">
          <v-toolbar-title
            class="text-center font-weight-bold"
            style="width: 100%; font-size: 16px"
          >
            المسافرون والدرجة السياحية
          </v-toolbar-title>
          <v-spacer></v-spacer>

          <v-btn icon @click="sheet = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-toolbar>
        <div class="py-3 grey lighten-4 pb-10" style="min-height: 100vh">
          <v-card elevation="0" class="mx-5">
            <v-card-title
              class="px-4 py-2"
              style="font-size: 15px; font-weight: 700"
            >
              المسافرون
            </v-card-title>
            <div class="d-flex justify-space-between px-4 py-3">
              <div>
                <span style="width: 50px" class="d-inline-block"> بالغ </span>
                <span class="grey--text text-lighten-3" style="font-size: 14px">
                  12 عام فأكثر
                </span>
              </div>

              <div class="d-flex align-baseline">
                <v-btn @click="quantity++" x-small outlined fab color="#FC8004">
                  <v-icon>mdi-plus</v-icon>
                </v-btn>
                <div style="width: 40px" class="text-center">
                  {{ quantity }}
                </div>
                <v-btn
                  @click="quantity--"
                  :disabled="quantity < 1"
                  x-small
                  fab
                  outlined
                  color="#FC8004"
                >
                  <v-icon>mdi-minus</v-icon>
                </v-btn>
              </div>
            </div>

            <div
              class="d-flex justify-space-between px-4 py-3"
              style="border-top: 1px solid rgb(241 241 241)"
            >
              <div>
                <span style="width: 50px" class="d-inline-block"> طفل </span>
                <span class="grey--text text-lighten-3" style="font-size: 14px">
                  2 - 11 عام
                </span>
              </div>

              <div class="d-flex align-baseline">
                <v-btn
                  @click="quantity2++"
                  x-small
                  outlined
                  fab
                  color="#FC8004"
                >
                  <v-icon>mdi-plus</v-icon>
                </v-btn>
                <div style="width: 40px" class="text-center">
                  {{ quantity2 }}
                </div>
                <v-btn
                  @click="quantity2--"
                  :disabled="quantity2 < 1"
                  x-small
                  fab
                  outlined
                  color="#FC8004"
                >
                  <v-icon>mdi-minus</v-icon>
                </v-btn>
              </div>
            </div>

            <div
              class="d-flex justify-space-between px-4 py-3"
              style="border-top: 1px solid rgb(241 241 241)"
            >
              <div>
                <span style="width: 50px" class="d-inline-block"> رضيع </span>
                <span class="grey--text text-lighten-3" style="font-size: 14px">
                  اقل من عامين
                </span>
              </div>

              <div class="d-flex align-baseline">
                <v-btn
                  @click="quantity3++"
                  x-small
                  outlined
                  fab
                  color="#FC8004"
                >
                  <v-icon>mdi-plus</v-icon>
                </v-btn>
                <div style="width: 40px" class="text-center">
                  {{ quantity3 }}
                </div>
                <v-btn
                  @click="quantity3--"
                  :disabled="quantity3 < 1"
                  x-small
                  fab
                  outlined
                  color="#FC8004"
                >
                  <v-icon>mdi-minus</v-icon>
                </v-btn>
              </div>
            </div>
          </v-card>

          <v-card elevation="0" class="my-4 mx-5">
            <v-card-title
              class="py-2"
              style="font-size: 15px; font-weight: 700"
            >
              الدرجة السياحية
            </v-card-title>
            <v-radio-group class="ma-0 pa-0" v-model="radioGroup">
              <div
                class="d-flex justify-space-between px-4 py-3"
                style="cursor: pointer"
                v-ripple
                @click="radioGroup = 'two'"
              >
                <div>
                  <span class="d-inline-block"> السياحية </span>
                </div>
                <v-radio
                  class="pa-0 ma-0"
                  value="two"
                  color="#FC8004"
                  :ripple="false"
                ></v-radio>
              </div>

              <div
                class="d-flex justify-space-between px-4 py-3"
                style="cursor: pointer; border-top: 1px solid rgb(241 241 241)"
                v-ripple
                @click="radioGroup = 'three'"
              >
                <div>
                  <span class="d-inline-block"> السياحية المتميزة </span>
                </div>
                <v-radio
                  class="pa-0 ma-0"
                  value="three"
                  color="#FC8004"
                  :ripple="false"
                ></v-radio>
              </div>

              <div
                class="d-flex justify-space-between px-4 py-3"
                style="cursor: pointer; border-top: 1px solid rgb(241 241 241)"
                @click="radioGroup = 'one'"
                v-ripple
              >
                <div>
                  <span class="d-inline-block"> رجال الاعمال </span>
                </div>
                <v-radio
                  class="pa-0 ma-0"
                  value="one"
                  color="#FC8004"
                  :ripple="false"
                ></v-radio>
              </div>
            </v-radio-group>
          </v-card>

          <div
            class="px-5 pt-3 pb-6 white shadow"
            style="position: absolute; bottom: 0; width: 100%; left: 0"
          >
            <p class="text-center mb-3 grey--text text--darken-2">
              3 مسافرين, الساحية
            </p>
            <v-btn
              block
              color="#FC8004"
              elevation="1"
              dark
              x-large
              class="rounded-lg py-6"
            >
              تأكيد
            </v-btn>
          </div>
        </div>
      </v-sheet>
    </v-bottom-sheet>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      tab: null,
      sheet: false,
      check: false,
      btns: 'one',
      radioGroup: 'one',
      quantity: 1,
      quantity2: 1,
      quantity3: 1,
      text:
        'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
      date: new Date().toISOString().substr(0, 10),
      date2: new Date().toISOString().substr(0, 10),
      menu: false,
      modal: false,
      menu2: false,
      place1: 'Istanbul airport',
      place2: 'Dubai airport',
    }
  },
  methods: {
    replace() {
      const x = this.place1
      this.place1 = this.place2
      this.place2 = x
    },
  },
}
</script>

<style  >
.v-tab {
  letter-spacing: 0 !important;
}
.v-tabs-slider-wrapper {
  height: 3px !important;
}
.v-tabs-slider {
  border-radius: 20px;
  margin: auto;
  width: calc(100% - 35px);
}
.v-slide-group__wrapper {
  -webkit-box-shadow: 2px -9px 5px -7px #f3f3f3;
  -moz-box-shadow: 2px -9px 5px -7px #f3f3f3;
  box-shadow: inset 2px -9px 5px -7px #f3f3f3;
}
.v-application--is-rtl .v-text-field .v-label {
  font-size: 14px !important;
  font-weight: 600 !important;
  color: #b0b0b0;
}
.v-input__slot:before,
.v-text-field > .v-input__control > .v-input__slot:after {
  display: none;
}
.v-text-field.v-text-field--enclosed:not(.v-text-field--rounded)
  > .v-input__control
  > .v-input__slot {
  border-radius: 10px;
  box-shadow: 1px 1px 5px #e7e7e7;
}
.v-input__prepend-inner {
  margin-left: 10px !important;
  /* color: #b0b0b0 !important; */
  color: red !important;
}
.v-input__icon i {
  color: #b0b0b0 !important;
}
.v-btn-toggle--group > .v-btn.v-btn {
  background-color: #f1f1f1 !important;
}

.travel-container {
  position: relative;
}
.travel-container:after {
  content: '';
  height: 0.5px;
  width: calc(100% - 100px);
  position: absolute;
  top: 0;
  margin: auto;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgb(233, 233, 233);
}
.v-text-field__details {
  display: none;
}
.v-sheet {
  border-radius: 20px !important;
}
.v-sheet .v-card {
  border-radius: 10px !important;
  box-shadow: 1px 1px 5px #e7e7e7 !important;
}
.v-dialog:not(.v-dialog--fullscreen) {
  max-height: 98%;
}
</style>