<template>
  <v-app>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer color="white" padless>
      <v-card width="100%" class="pb-1">
        <v-tabs v-model="tab" color="#FC8004" centered icons-and-text>
          <v-tab href="#tab-1" class="font-weight-bold">
            بحث
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="22"
              height="22"
              fill="currentColor"
              class="bi bi-search mx-2"
              viewBox="0 0 16 16"
            >
              <path
                d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"
              />
            </svg>
          </v-tab>

          <v-tab href="#tab-2" class="font-weight-bold">
            طلباتي
            <v-icon>mdi-book-open</v-icon>
          </v-tab>

          <v-tab href="#tab-3" class="font-weight-bold">
            متطلبات التأشيرة
            <v-icon>mdi-order-bool-ascending-variant</v-icon>
          </v-tab>

          <v-tab href="#tab-4" class="font-weight-bold">
            المزيد
            <v-icon>mdi-dots-horizontal</v-icon>
          </v-tab>
        </v-tabs>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
export default {}
</script>
