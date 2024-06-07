<template>
  <v-container class="justify-center mt-5">
    <TabelaDados @editItem="editItem" @abrirDialog="() => ativo = true" titulo="Coupons" :loading="loading" @deleteItem="deleteItem" :headers="headers" :items="items"></TabelaDados>
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
              v-model="cupons.id"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Code"
              placeholder="Code"
              v-model="cupons.code"
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Type"
              placeholder="Type"
              v-model="cupons.type"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Value"
              placeholder="Value"
              v-model="cupons.value"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Uses"
              placeholder="Uses"
              v-model="cupons.uses"
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
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
      cupons: {
        id: null,
        code: null,
        type: null,
        value: null,
        uses: null,
      },
      headers: [
        {
          title: 'ID',
          key: 'id'
        },
        {
          title: 'Code',
          key: 'code'
        },
        {
          title: 'Type',
          key: 'type'
        },
        {
          title: 'Value',
          key: 'value'
        },
        {
          title: 'Uses',
          key: 'uses'
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
      return this.cupons.id ? 'Editar': 'Criar';
    }
  },

  watch: {
    ativo(valor) {
      if (valor == false) {
        this.resetCupons()
      }
    }
  },

  methods: {
    resetCupons() {
      this.cupons = {
        id: null,
        code: null,
        type: null,
        value: null,
        uses: null,
        idCategory: null
      }
      this.ativo = false;
    },

    async create() {
      if(this.cupons.id){
        const response = await this.$api.patch(`/cupons/${this.cupons.id}`, this.cupons);
      }
      else{
        await this.$api.post('/cupons', this.cupons);
      }
      this.resetCupons()
      await this.getItems();
    },

    editItem(item) {
      this.cupons = {
        ...item
      };
      this.ativo = true;
    },

    async edit() {
      const response = await this.$api.patch(`/cupons/${this.cupons.id}`, this.cupons);
      this.resetCupons()
      await this.getItems();
    },

    async deleteItem(item) {
      if (confirm(`Deseja deletar o registro com id ${item.id}`)) {
        const response = await this.$api.delete(`/cupons/${item.id}`);
        if (response.type == 'error') {
          alert(response.message);
        }
      }
      await this.getItems();
    },

    async getItems() {
      const response = await this.$api.get('/cupons');
      this.items = response.response;
      this.loading = false;
    }
  }
}
</script>
