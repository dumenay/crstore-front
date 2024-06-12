<template>
    <v-app>
        <Header/>
    <v-container
    style="overflow-y: scroll; max-height: 100dvh; width: 100dvw; margin-top: 20px;">
        <v-row>
        <CardProdutos
            :items="items"
        />
        </v-row>
    </v-container>
    </v-app>
</template>

<script>
import CardProdutos from '~/components/CardProdutos.vue';

export default {
  data: () => {
    return {
      dialog: false,
      valor: 0,
      ativo: false,
      loading: true,
      textoUsuario: null,
      products: {
        id: null,
        name: null,
        price: null,
        image: null,
        description: null,
        idCategory: null
      },
      headers: [
        {
          title: 'ID',
          key: 'id'
        },
        {
          title: 'Name',
          key: 'name'
        },
        {
          title: 'Price',
          key: 'price'
        },
        {
          title: 'Description',
          key: 'description'
        },
        {
          title: 'Category',
          key: 'idCategory'
        },
        {
          title: 'Actions',
          key: 'actions',
          sortable: false
        },
      ],
      items: [],
    }
  },

  async created(){
    await this.getItems();
  },


  methods: {
   async getItems() {
      const response = await this.$api.get('/products');
      this.items = response.response;
      this.loading = false;
    }
  }
}
</script>
