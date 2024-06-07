<template>
  <v-container class="justify-center mt-5">
    <TabelaDados @editItem="editItem" @abrirDialog="() => ativo = true" titulo="Payments" :loading="loading" @deleteItem="deleteItem" :headers="headers" :items="items"></TabelaDados>
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
              v-model="payments.id"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Name"
              placeholder="Name"
              v-model="payments.name"
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
      payments: {
        id: null,
        name: null
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
          title: 'Actions',
          key: 'actions',
          sortable: false
        },
      ],
      items: [],
      //payments: [],
    }
  },

  async created(){
    await this.getItems();
  },

  computed: {
    tituloDialog: function() {
      return this.payments.id ? 'Editar': 'Criar';
    }
  },

  watch: {
    ativo(valor) {
      if (valor == false) {
        this.resetPayments()
      }
    }
  },

  methods: {
    resetPayments() {
      this.payments = {
        id: null,
        name: null
      }
      this.ativo = false;
    },

    async create() {
      if(this.payments.id){
        const response = await this.$api.patch(`/payments/${this.payments.id}`, this.payments);
      }
      else{
        await this.$api.post('/payments', this.payments);
      }
      this.resetPayments()
      await this.getItems();
    },

    editItem(item) {
      this.payments = {
        ...item
      };
      this.ativo = true;
    },

    async edit() {
      const response = await this.$api.patch(`/payments/${this.payments.id}`, this.payments);
      this.resetPayments()
      await this.getItems();
    },

    async deleteItem(item) {
      if (confirm(`Deseja deletar o registro com id ${item.id}`)) {
        const response = await this.$api.delete(`/payments/${item.id}`);
        if (response.type == 'error') {
          alert(response.message);
        }
      }
      await this.getItems();
    },


    async getItems() {
      const response = await this.$api.get('/payments');
      this.items = response.response;
      this.loading = false;
    }
  }
}
</script>
