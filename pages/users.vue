<template>
  <v-container class="justify-center mt-5">
    <TabelaDados @editItem="editItem" @abrirDialog="() => ativo = true" titulo="Users" :loading="loading" @deleteItem="deleteItem" :headers="headers" :items="items"></TabelaDados>
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
              v-model="users.id"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Name"
              placeholder="Name"
              v-model="users.name"
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Username"
              placeholder="Username"
              v-model="users.username"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Password"
              placeholder="Password"
              v-model="users.passwordHash"
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="CPF"
              placeholder="CPF"
              v-model="users.cpf"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Token"
              placeholder="Token"
              v-model="users.token"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-combobox
              label="Role"
              :items="['Client', 'Deliverer', 'Admin']"
              variant="outlined"
              v-model="users.role"
            ></v-combobox>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              variant="outlined"
              label="E-Mail"
              placeholder="E-Mail"
              v-model="users.email"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-text-field
              variant="outlined"
              label="Phone"
              placeholder="Phone Number"
              v-model="users.phone"
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
      users: {
        id: null,
        username: null,
        passwordHash: null,
        name: null,
        email: null,
        cpf: null,
        phone: null,
        role: null
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
          title: 'Email',
          key: 'email'
        },
        {
          title: 'Phone Number',
          key: 'phone'
        },
        {
          title: 'Role',
          key: 'role'
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
      return this.users.id ? 'Editar': 'Criar';
    }
  },

  watch: {
    ativo(valor) {
      if (valor == false) {
        this.resetUsers()
      }
    }
  },

  methods: {
    resetUsers() {
      this.users = {
        id: null,
        name: null,
        email: null,
        phone: null,
        role: null
      }
      this.ativo = false;
    },

    async create() {
      if(this.users.id){
        const response = await this.$api.patch(`/users/${this.users.id}`, this.users);
      }
      else{
        console.log(this.users)
        await this.$api.post('/users', this.users);
      }
      this.resetUsers()
      await this.getItems();
    },

    editItem(item) {
      this.users = {
        ...item
      };
      this.ativo = true;
    },

    async edit() {
      const response = await this.$api.patch(`/users/${this.users.id}`, this.users);
      this.resetUsers()
      await this.getItems();
    },

    async deleteItem(item) {
      if (confirm(`Deseja deletar o registro com id ${item.id}`)) {
        const response = await this.$api.delete(`/users/${item.id}`);
        if (response.type == 'error') {
          alert(response.message);
        }
      }
      await this.getItems();
    },


    async getItems() {
      const response = await this.$api.get('/users');
      this.items = response.response;
      this.loading = false;
    }
  }
}
</script>
