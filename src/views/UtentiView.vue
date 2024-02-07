<template>
  <div class="d-flex flex-column align-center justify-center" style="height: 100vh; width: 100%; padding-top: 80px;">
    <v-app>
      <v-container>
        <v-row class="mt-1">
          <v-col v-for="item in utenti" :key="item.id" cols="12" sm="6" md="4" lg="3">
            <v-card block @click="openDialog(item.id)">
              <v-img :src="item.image" height="150"></v-img>
              <v-card-title>{{ item.firstName }} {{ item.lastName }}</v-card-title>
              <v-card-text>{{ item.email }}</v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
      <div class="text-center">
        <v-dialog v-model="dialog" activator="parent" width="auto">
          <v-card>
            <v-card-text>
              <v-sheet border>
                <v-img
                  :gradient="`to top right, rgba(255, 255, 255, .1), rgba(255, 255, 255 .15)`"
                  :src="utenti[id_about].image"
                  cover
                  height="150"
                ></v-img>

                <v-list-item
                  :title="utenti[id_about].username"
                  lines="two"
                  density="comfortable"
                  :subtitle="utenti[id_about].firstName"
                >
                  <template v-slot:title>
                    <strong class="text-h6">
                      {{ utenti[id_about].lastName }}
                    </strong>
                  </template>
                </v-list-item>

                <v-table density="compact" class="text-caption">
                  <tbody>
                    <tr align="right">
                      <th>Age:</th>
                      <td>{{ utenti[id_about].age }}</td>
                    </tr>
                    <tr align="right">
                      <th>Gender:</th>
                      <td>{{ utenti[id_about].gender }}</td>
                    </tr>
                    <tr align="right">
                      <th>Phone:</th>
                      <td>{{utenti[id_about].phone }}</td>
                    </tr>
                    <tr align="right">
                      <th>Birthdate:</th>
                      <td>{{ utenti[id_about].birthDate }}</td>
                    </tr>
                  </tbody>
                </v-table>
              </v-sheet>
            </v-card-text>
            <v-card-actions>
              <v-btn color="red-darken-4" block @click="dialog = false">CLOSE</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
    </v-app>
  </div>
</template>

<script>
import utenti from '../utenti.js'

export default {
    name: 'UtentiView',
    data() {
        return {
            utenti: [],
            dialog: false,
            id_about: 0
        }
    },
    methods: {
        openDialog(id) {
            this.id_about = id-1; // Corrected line
            this.dialog = true
            return this.id_about; // Corrected line
        }
    },
    mounted() {
        this.utenti = utenti
    }
}
</script>
