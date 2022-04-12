<template>

    <div>
        <v-container class="grey lighten-5">
            <v-row no-gutters>
            <v-col
                cols="12"
                md="4"
                offset-md="4"
                sm="4"
            >
                <validation-observer
                    ref="observer"
                    v-slot="{ invalid }"
                >
                    <form @submit.prevent="submit">
                    <validation-provider
                        v-slot="{ errors }"
                        name="Name"
                        rules="required|max:10"
                    >
                        <v-text-field
                        v-model="name"
                        :counter="10"
                        :error-messages="errors"
                        label="Name"
                        required
                        ></v-text-field>
                    </validation-provider>

                    <validation-provider
                        v-slot="{ errors }"
                        name="phoneNumber"
                        :rules="{
                        required: true,
                        digits: 7,
                        regex: '^(71|72|74|76|81|82|84|85|86|87|88|89)\\d{5}$'
                        }"
                    >
                        <v-text-field
                        v-model="phoneNumber"
                        :counter="7"
                        :error-messages="errors"
                        label="Phone Number"
                        required
                        ></v-text-field>
                    </validation-provider>

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

                    <validation-provider
                        v-slot="{ errors }"
                        name="select"
                        rules="required"
                    >
                        <v-select
                        v-model="select"
                        :items="items"
                        :error-messages="errors"
                        label="Select"
                        data-vv-name="select"
                        required
                        ></v-select>
                    </validation-provider>
                    
                    <validation-provider
                        v-slot="{ errors }"
                        rules="required"
                        name="checkbox"
                    >
                        <v-checkbox
                        v-model="checkbox"
                        :error-messages="errors"
                        value="1"
                        label="Option"
                        type="checkbox"
                        required
                        ></v-checkbox>
                    </validation-provider>

                    <v-btn
                        class="mr-4"
                        type="submit"
                        :disabled="invalid"
                    >
                        submit
                    </v-btn>
                    <v-btn @click="clear">
                        clear
                    </v-btn>
                    </form>
                </validation-observer>

            </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>

import { ValidationObserver, ValidationProvider } from "vee-validate";
  export default {
    components: {
      ValidationProvider,
      ValidationObserver,
    },
    data: () => ({
      name: '',
      phoneNumber: '',
      email: '',
      select: null,
      items: [
        'Item 1',
        'Item 2',
        'Item 3',
        'Item 4',
      ],
      checkbox: null,
    }),

    methods: {
      submit () {
        this.$refs.observer.validate()
      },
      clear () {
        this.name = ''
        this.phoneNumber = ''
        this.email = ''
        this.select = null
        this.checkbox = null
        this.$refs.observer.reset()
      },
    },
  }
</script>