<template>
  <v-container fluid>
    <v-card>
      <v-toolbar dense flat color="deep-purple accent-2" dark>
        <v-toolbar-title>주간보고</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-icon>mdi-eye</v-icon>
      </v-toolbar>
      <v-card-text>
        <v-row>
          <v-col cols="12" sm="6">
            <v-select
              v-model="category"
              :items="categoryItems"
              hide-details
              outlined>
            </v-select>
          </v-col>
          <v-col cols="12" sm="6">
            <v-menu
              v-model="menu"
              :close-on-content-click="false"
              :nudge-right="40"
              transition="scale-transition"
              offset-y
              min-width="290px"
            >
              <template v-slot:activator="{ on }">
                <v-text-field
                  v-model="date"
                  label="Picker without buttons"
                  prepend-inner-icon="mdi-calendar"
                  readonly
                  v-on="on"
                  hide-details
                  outlined
                ></v-text-field>
              </template>
              <v-date-picker v-model="date" @input="menu = false"></v-date-picker>
            </v-menu>
          </v-col>
          <v-col cols="12" sm="6" v-for="i in 2" :key="i">
            <v-card>
              <v-subheader>지난주</v-subheader>
              <v-divider></v-divider>
              <v-list-item three-line>
                <v-list-item-content>
                  <v-list-item-title>
                    가나다라마바사
                  </v-list-item-title>
                  <v-list-item-subtitle>
                    ijwiejgiojwoejgiawje;ofijawi;erja;lweira;lweijra;lwiejr;awefweflwiejrwegweg
                  </v-list-item-subtitle>
                </v-list-item-content>
                <v-list-item-icon>
                  <v-progress-circular
                    :rotate="270"
                    :size="50"
                    :width="10"
                    :value="25"
                    color="pink"
                  >
                    100
                  </v-progress-circular>

                </v-list-item-icon>
              </v-list-item>
              <v-divider></v-divider>
              <v-list-item three-line>
                <v-list-item-content>
                  <v-list-item-title>
                    가나다라마바사
                  </v-list-item-title>
                  <v-list-item-subtitle>
                    ijwiejgiojwoejgiawje;ofijawi;erja;lweira;lweijra;lwiejr;awefweflwiejrwegweg
                  </v-list-item-subtitle>
                </v-list-item-content>
                <v-list-item-icon>
                  <v-progress-circular
                    :rotate="270"
                    :size="50"
                    :width="10"
                    :value="40"
                    color="pink"
                  >
                    40
                  </v-progress-circular>

                </v-list-item-icon>
              </v-list-item>
              <v-divider></v-divider>
              <v-list-item three-line>
                <v-list-item-content>
                  <v-list-item-title>
                    가나다라마바사
                  </v-list-item-title>
                  <v-list-item-subtitle>
                    ijwiejgiojwoejgiawje;ofijawi;erja;lweira;lweijra;lwiejr;awefweflwiejrwegweg
                  </v-list-item-subtitle>
                </v-list-item-content>
                <v-list-item-icon>
                  <v-progress-circular
                    :rotate="270"
                    :size="50"
                    :width="10"
                    :value="25"
                    color="pink"
                  >
                    25
                  </v-progress-circular>

                </v-list-item-icon>
              </v-list-item>

            </v-card>
          </v-col>

        </v-row>

      </v-card-text>
    </v-card>
  </v-container>
</template>
<script>
export default {
  data () {
    return {
      menu: false,
      date: this.$moment().format('YYYY-MM-DD'),
      category: '생산',
      categoryItems: ['연구소', '생산', 'QC']
    }
  }
}
</script>
