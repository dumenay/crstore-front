<template>
    <v-app>
        <Header/>
        <v-container style="position: absolute; left: 30%; top: 8%">
            <v-card
            height="820"
            width="600"
            >
            <v-card-title>
                <h1
                style="text-align: center;">
                    Registro
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
                    label="Password"
                    placeholder="Password"
                    >
                    </v-text-field>
                </v-col>
                </v-row>
                <v-row
                style="margin-top: 15px;">
                <v-col>
                    <v-text-field
                    variant="outlined"
                    label="E-Mail"
                    placeholder="E-Mail"
                    >
                    </v-text-field>
                </v-col>
                </v-row>
                <v-row
                style="margin-top: 15px;">
                <v-col>
                    <v-text-field
                    variant="outlined"
                    label="CPF"
                    placeholder="CPF"
                    >
                    </v-text-field>
                </v-col>
                <v-col>
                    <v-text-field
                    variant="outlined"
                    label="Phone Number"
                    placeholder="Phone Number"
                    >
                    </v-text-field>
                </v-col>
                </v-row>
                <v-row
                style="margin-top: 15px;">
                <v-col>
                    <v-combobox
                    label="Role"
                    :items="['Client', 'Deliverer']"
                    variant="outlined"
                    ></v-combobox>
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
            </v-card-text>
            <v-card-actions>
                <v-spacer/>
                <v-btn
                text="Register"
                style="margin-right: 30px; width: 100px; height: 45px;"
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