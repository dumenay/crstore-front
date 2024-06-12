<template>
    <v-card
      v-for="(item, i) in items"
      class="mx-auto my-12"
      width="350"
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
        :src= "item.image"
        cover
      />
  
        <v-card-text
        style="font-size: 22px; font-weight: bold;">
        {{  item.name  }}</v-card-text>
  
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
          R$ {{ item.price.replace(".", ",") }}
        </div>
  
        <div>{{ item.description }}</div>
      </v-card-text>
  
      <v-divider class="mx-4 mb-1"></v-divider>
  
      <v-card-actions>
        <v-btn
          text="Adicionar ao Carrinho"
          block
          variant="tonal"
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

  props: {
    items: []
  },

  methods: {
    
  },
}
</script>