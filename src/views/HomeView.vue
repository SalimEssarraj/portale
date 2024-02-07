<template>
  <div class="align-center justify-center" style="height: 100vh; width: auto; padding-top: 20vh;">
    <v-card class="mx-auto pa-12 pb-8" elevation="8" max-width="448" rounded="lg">

      <h1 :class="[cls, 'pa-4']">Log-in form</h1>
      <br>

      <v-sheet width="300" class="mx-auto">
        <v-form ref="form">
          <v-text-field :rules="rulesE" label="E-mail" id="E-mail"></v-text-field>
          <br>
          <v-text-field v-model="password" :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
            :rules="[rules.required, rules.min]" :type="show1 ? 'text' : 'password'" name="input-10-1" label="password"
            hint="At least 8 characters" counter @click:append="show1 = !show1" id="pwd"></v-text-field>

          <div class="d-flex flex-column">
            <v-btn color="success" class="mt-4" block >
              Sign in
            </v-btn>

            <v-btn color="error" class="mt-4" block @click="goRegister">Register a new account</v-btn>
          </div>
        </v-form>
      </v-sheet>
    </v-card>
  </div>
</template>

<script>
import utenti from '../utenti.js'

export default {
  data: () => ({
    //return :{
    show1: false,
    show2: true,
    password: '',
    rules: {
      required: value => !!value || 'Required.',
      min: v => v.length >= 8 || 'Min 8 characters',
      emailMatch: () => `The email and password you entered don't match`,
    },
    //},

    rulesE: [
      value => !!value || 'Required.',
      value => (value || '').length <= 20 || 'Max 20 characters',
      value => {
        const pattern =
          /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
        return pattern.test(value) || 'Invalid e-mail.'
      },
    ],

    email: "",
    pwd: "",
    utenti: []
  }),

  methods: {
  goRegister(){
    console.log("CIAO")
    this.$router.push({ name: 'register' });
  }
  },
  mounted() { 
      this.utenti = utenti
  }
}
</script>