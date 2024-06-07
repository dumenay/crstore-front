<template>
  <v-container class="justify-center mt-5">
    <TabelaDados @editItem="editItem" @abrirDialog="() => ativo = true" titulo="Products" :loading="loading" @deleteItem="deleteItem" :headers="headers" :items="items"></TabelaDados>
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
              v-model="products.id"
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Name"
              placeholder="Name"
              v-model="products.name"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Category"
              placeholder="Category"
              v-model="products.idCategory"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Price"
              placeholder="Price"
              v-model="products.price"
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Image"
              placeholder="Image"
              v-model="products.image"
            >
            </v-text-field>
          </v-col>
          <v-col>
                <img :src="products.image" style="max-width: 100px; max-height: 100px">
              </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Description"
              placeholder="Description"
              v-model="products.description"
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

  computed: {
    tituloDialog: function() {
      return this.products.id ? 'Editar': 'Criar';
    }
  },

  watch: {
    ativo(valor) {
      if (valor == false) {
        this.resetProducts()
      }
    }
  },

  methods: {
    resetProducts() {
      this.products = {
        id: null,
        name: null,
        price: null,
        image: null,
        description: null,
        idCategory: null
      }
      this.ativo = false;
    },

    async create() {
      if(this.products.id){
        const response = await this.$api.patch(`/products/${this.products.id}`, this.products);
      }
      else{
        await this.$api.post('/products', this.products);
      }
      this.resetProducts()
      await this.getItems();
    },

    editItem(item) {
      this.products = {
        ...item
      };
      this.ativo = true;
    },

    async edit() {
      const response = await this.$api.patch(`/products/${this.products.id}`, this.products);
      this.resetProducts()
      await this.getItems();
    },

    async deleteItem(item) {
      if (confirm(`Deseja deletar o registro com id ${item.id}`)) {
        const response = await this.$api.delete(`/products/${item.id}`);
        if (response.type == 'error') {
          alert(response.message);
        }
      }
      await this.getItems();
    },


    async getItems() {
      const response = await this.$api.get('/products');
      this.items = response.response;
      this.loading = false;
    }
  }
}
</script>
