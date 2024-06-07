<template>
  <v-container class="justify-center mt-5">
    <TabelaDados @editItem="editItem" @abrirDialog="() => ativo = true" titulo="Orders Products" :loading="loading" @deleteItem="deleteItem" :headers="headers" :items="items"></TabelaDados>
  </v-container>
  <v-dialog
      v-model="ativo"
      max-width="500"
    >
    <v-card
      height="600"
      width="700"
    >
      <v-card-title>
        <h1>
          {{ tituloDialog }}
        </h1>
      </v-card-title>
      <v-card-text>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="ID"
              placeholder="ID"
              disabled
              v-model="ordersProducts.id"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Price Products"
              placeholder="Price Products"
              v-model="ordersProducts.priceProducts"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
            variant="outlined"
            label="Quantity"
            placeholder="Quantity"
            v-model="ordersProducts.quantity"
            >
          </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="ID Order"
              placeholder="ID Order"
              v-model="ordersProducts.idOrder"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="ID Product"
              placeholder="ID Product"
              v-model="ordersProducts.idProduct"
            >
            </v-text-field>
          </v-col>
        </v-row>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          color="green"
          variant="outlined"
          @click="create"
        >
          Confirm
        </v-btn>
      </v-card-actions>
    </v-card>
    </v-dialog>
</template>

<script>
export default {
  data: () => {
    return {
      dialog: false,
      valor: 0,
      ativo: false,
      loading: true,
      textoUsuario: null,
      ordersProducts: {
        id: null,
        priceProducts: null,
        quantity: null,
        idOrder: null,
        idProduct: null,
      },
      headers: [
        {
          title: 'ID',
          key: 'id'
        },
        {
          title: 'Price Products',
          key: 'priceProducts'
        },
        {
          title: 'Quantity',
          key: 'quantity'
        },
        {
          title: 'ID Order',
          key: 'idOrder'
        },
        {
          title: 'ID Product',
          key: 'idProduct'
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

  computed: {
    tituloDialog: function() {
      return this.ordersProducts.id ? 'Editar': 'Criar';
    }
  },

  watch: {
    ativo(valor) {
      if (valor == false) {
        this.resetOrdersProducts()
      }
    }
  },

  methods: {
    resetOrdersProducts() {
      this.ordersProducts = {
        id: null,
        priceProducts: null,
        quantity: null,
        idOrder: null,
        idProduct: null
      }
      this.ativo = false;
    },

    async create() {
      if(this.ordersProducts.id){
        const response = await this.$api.patch(`/ordersProducts/${this.ordersProducts.id}`, this.ordersProducts);
      }
      else{
        await this.$api.post('/ordersProducts', this.ordersProducts);
      }
      this.resetOrdersProducts()
      await this.getItems();
    },

    editItem(item) {
      this.ordersProducts = {
        ...item
      };
      this.ativo = true;
    },

    async edit() {
      const response = await this.$api.patch(`/ordersProducts/${this.ordersProducts.id}`, this.ordersProducts);
      this.resetOrdersProducts()
      await this.getItems();
    },

    async deleteItem(item) {
      if (confirm(`Deseja deletar o registro com id ${item.id}`)) {
        const response = await this.$api.delete(`/ordersProducts/${item.id}`);
        if (response.type == 'error') {
          alert(response.message);
        }
      }
      await this.getItems();
    },


    async getItems() {
      const response = await this.$api.get('/ordersProducts');
      this.items = response.response;
      this.loading = false;
    }
  }
}
</script>
