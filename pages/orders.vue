<template>
  <v-container class="justify-center mt-5">
    <TabelaDados @editItem="editItem" @abrirDialog="() => ativo = true" titulo="Orders" :loading="loading" @deleteItem="deleteItem" :headers="headers" :items="items"></TabelaDados>
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
              v-model="orders.id"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Status"
              placeholder="Status"
              v-model="orders.status"
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Total"
              placeholder="Total"
              v-model="orders.total"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Discount"
              placeholder="Discount"
              v-model="orders.totalDiscount"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Coupon"
              placeholder="Coupon"
              v-model="orders.idCupom"
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Customer"
              placeholder="Customer"
              v-model="orders.idUserCustomer"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Deliverer"
              placeholder="Deliverer"
              v-model="orders.idUserDeliver"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Address"
              placeholder="Address"
              v-model="orders.idAddress"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Payment"
              placeholder="Payment"
              v-model="orders.idPayment"
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
      orders: {
        id: null,
        status: null,
        total: null,
        totalDiscount: null,
        idUserCustomer: null,
        idUserDeliver: null,
        idAddress: null,
        idPayment: null,
        idCupom: null
      },
      headers: [
        {
          title: 'ID',
          key: 'id'
        },
        {
          title: 'Status',
          key: 'status'
        },
        {
          title: 'Price',
          key: 'total'
        },
        {
          title: 'Discount',
          key: 'totalDiscount'
        },
        {
          title: 'Coupon',
          key: 'idCupom'
        },
        {
          title: 'Customer',
          key: 'idUserCustomer'
        },
        {
          title: 'Deliverer',
          key: 'idUserDeliver'
        },
        {
          title: 'Address',
          key: 'idAddress'
        },
        {
          title: 'Payment',
          key: 'idPayment'
        },
        {
          title: 'Actions',
          key: 'actions',
          sortable: false
        },
      ],
      items: [],
      orders: [],
    }
  },

  async created(){
    await this.getItems();
  },

  computed: {
    tituloDialog: function() {
      return this.orders.id ? 'Editar': 'Criar';
    }
  },

  watch: {
    ativo(valor) {
      if (valor == false) {
        this.resetOrders()
      }
    }
  },

  methods: {
    resetOrders() {
      this.orders = {
        id: null,
        status: null,
        total: null,
        totalDiscount: null,
        idUserCustomer: null,
        idUserDeliver: null,
        idAddress: null,
        idPayment: null,
        idCupom: null
      }
      this.ativo = false;
    },

    async create() {
      if(this.orders.id){
        const response = await this.$api.patch(`/orders/${this.orders.id}`, this.orders);
      }
      else{
        await this.$api.post('/orders', this.orders);
      }
      this.resetOrders()
      await this.getItems();
    },

    editItem(item) {
      this.orders = {
        ...item
      };
      this.ativo = true;
    },

    async deleteItem(item) {
      if (confirm(`Deseja deletar o registro com id ${item.id}`)) {
        const response = await this.$api.delete(`/orders/${item.id}`);
        if (response.type == 'error') {
          alert(response.message);
        }
      }
      await this.getItems();
    },


    async getItems() {
      const response = await this.$api.get('/orders');
      this.items = response.response;
      this.loading = false;
    }
  }
}
</script>
