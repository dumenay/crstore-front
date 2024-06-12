<template>
    <v-app>
        <Header/>
        <v-container style="position: absolute; left: 30%; top: 20%">
            <v-card
            height="500"
            width="600"
            >
            <v-card-title style="margin-top: 40px;">
                <h1
                style="text-align: center;">
                    Login
                </h1>
            </v-card-title>
            <v-card-text>
                <v-row
                style="margin-top: 15px;">
                <v-col>
                    <v-text-field
                    variant="outlined"
                    label="Username"
                    placeholder="Username"
                    >
                    </v-text-field>
                </v-col>
                </v-row>
                <v-row
                style="margin-top: 15px;">
                <v-col>
                    <v-text-field
                    variant="outlined"
                    label="Senha"
                    placeholder="Senha"
                    >
                </v-text-field>
                </v-col>
                </v-row>
                    <v-text
                    style="margin-left: 400px;" @click="">
                        Esqueceu Sua Senha?
                    </v-text>
            </v-card-text>
            <v-card-actions>
                <v-spacer/>
                <v-btn
                text="Login"
                style="margin-top: 15px; margin-right: 30px; width: 100px; height: 45px;"
                color="green"
                variant="tonal"
                elevation="8"
                @click=""
                />
            </v-card-actions>
            </v-card>
        </v-container>
    </v-app>
</template>

<script>
export default {
}
</script>