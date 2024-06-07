<template>
    <v-card
      class="mx-auto my-12"
      max-width="330"
    >
      <template v-slot:loader="{ isActive }">
        <v-progress-linear
          :active="isActive"
          height="4"
          indeterminate
        ></v-progress-linear>
      </template>
  
      <v-img
        height="200"
        src="https://cdn.vuetifyjs.com/images/cards/cooking.png"
        cover
      ></v-img>
  
      <v-card-item>
        <v-card-title>Nome Produto</v-card-title>
      </v-card-item>
  
      <v-card-text>
        <v-row
          class="mx-0"
        >
          <v-rating
            :model-value="4.5"
            color="amber"
            density="compact"
            size="small"
            half-increments
            readonly
          ></v-rating>
  
          <div class="text-grey ms-4">
            Avaliação 4.5 (413)
          </div>
        </v-row>
  
        <div class="my-4 text-subtitle-1">
          Valor
        </div>
  
        <div>Small plates, salads & sandwiches - an intimate setting with 12 indoor seats plus patio seating.</div>
      </v-card-text>
  
      <v-divider class="mx-4 mb-1"></v-divider>
  
      <v-card-actions>
        <v-btn
          text="Reserve"
          block
          variant="outlined"
          @click=""
        ></v-btn>
      </v-card-actions>
    </v-card>
  </template>

<script>
export default {
  data: () => ({
    loading: false,
    selection: 1,
  }),

  methods: {
    
  },
}
</script>