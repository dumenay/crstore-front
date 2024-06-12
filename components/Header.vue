<template>
    <v-app-bar>
            <v-row>
                <v-spacer/>
                <v-spacer/>
                <v-col cols="auto">
                    <v-btn href="/" class="mx-2" variant="text">
                        Home
                    </v-btn>
                    <v-btn href="/categorias" class="mx-2" variant="text">
                        Categorias
                    </v-btn>
                    <v-btn href="/produtos" class="mx-2" variant="text">
                        Produtos
                    </v-btn>
                </v-col>
                <v-spacer></v-spacer>
                <v-col>
                    <v-btn
                        text="Login"
                        class="mx-3" variant="outlined"
                        href="/login"
                    />
                    <v-btn 
                        text="Registro"
                        class="mx-3" variant="outlined"
                        href="/register"
                    />
                </v-col>
            </v-row>
        </v-app-bar>
</template>

<script>
export default{
    
} 
</script>