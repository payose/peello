<template>
    <div class="d-flex fill-height align-center">
        <v-container class="fill-height">
            
            <v-snackbar
            :timeout="5000"
            :value="show"
            absolute
            centered
            right
            tile
            color="red accent-2"
            >
                email or password incorrect
            </v-snackbar>
            <v-row no-gutters>
            <v-col
                cols="12"
                md="4"
                offset-md="4"
                sm="4"
            >

                <v-card outlined shaped class="pa-6"
                >
                    <validation-observer
                        ref="observer"
                        v-slot="{ invalid }"
                    >   
                        <v-card-title>Sign in</v-card-title>

                        <form @submit.prevent="signin">

                            <!-- EMAIL -->
                            <validation-provider
                                v-slot="{ errors }"
                                name="email"
                                rules="required|email"
                            >
                                <v-text-field
                                v-model="email"
                                :error-messages="errors"
                                label="E-mail"
                                required
                                ></v-text-field>
                            </validation-provider>

                            <!-- PASSWORD -->
                            <validation-provider
                                v-slot="{ errors }"
                                rules="required"
                            >
                                <v-text-field
                                v-model="password"
                                :error-messages="errors"
                                label="Password"
                                required
                                ></v-text-field>
                            </validation-provider>

                            <v-btn
                                class="mr-4"
                                type="submit"
                                :disabled="invalid"
                            >
                                Signin
                            </v-btn>
                            
                        </form>
                    </validation-observer>
                </v-card>
            </v-col>
            </v-row>

        </v-container>
    </div>
</template>

<script>
import { ValidationObserver, ValidationProvider } from "vee-validate";
  export default {
    layout: 'auth',
    components: {
      ValidationProvider,
      ValidationObserver,
    },
    data(){
        return{
            email: '',
            password: '',
            show: false
   
        }
    },

    methods: {
        signin () {
            this.$refs.observer.validate()
            this.$fire.auth.signInWithEmailAndPassword(this.email, this.password)
            .then((user) => $nuxt.$router.push('/'))
            .catch (this.show = true)
            
        },

      clear () {
        this.email = ''
        this.password = ''
        this.$refs.observer.reset()
      },
    },
  }
</script>