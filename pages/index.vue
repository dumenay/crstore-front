<template>
    <v-app-bar>
        <v-row>
            <v-spacer></v-spacer>
            <v-spacer></v-spacer>
            <v-col cols="auto">
                <v-btn @click="" class="mx-2" variant="text">
                    Home
                </v-btn>
                <v-btn class="mx-2" variant="text">
                    Categorias
                </v-btn>
                <v-btn class="mx-2" variant="text">
                    Produtos
                </v-btn>
            </v-col>
            <v-spacer></v-spacer>
            <v-col>
                <v-btn class="mx-3" variant="outlined">
                    Login
                </v-btn>
                <v-btn class="mx-3" variant="outlined">
                    Registro
                </v-btn>
            </v-col>
        </v-row>
    </v-app-bar>
    <v-body>
        <v-row>
        <CardProdutos></CardProdutos>
        </v-row>
    </v-body>
</template>

<script>
export default {
}
</script>
