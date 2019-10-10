<template>
  <v-container fluid>
    <v-card>
      <v-toolbar dense flat color="deep-purple accent-2" dark>
        <v-toolbar-title>주간보고</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn icon @click="edit = !edit">
          <v-icon>{{edit ? 'mdi-eye' : 'mdi-pencil'}}</v-icon>
        </v-btn>
      </v-toolbar>
      <v-card-text>
        <v-row>
          <v-col cols="12" sm="6">
            <v-select
              v-model="report.category"
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
                  v-model="report.date"
                  label="Picker without buttons"
                  prepend-inner-icon="mdi-calendar"
                  readonly
                  v-on="on"
                  hide-details
                  outlined
                ></v-text-field>
              </template>
              <v-date-picker v-model="report.date" @input="menu = false"></v-date-picker>
            </v-menu>
          </v-col>
        </v-row>
        <write :report="report" v-if="edit" @editFalse="edit = false"></write>
        <read :report="report" v-else></read>
      </v-card-text>
    </v-card>
  </v-container>
</template>
<script>
import read from './read'
import write from './write'
export default {
  components: { read, write },
  data () {
    return {
      menu: false,
      categoryItems: ['연구소', '생산', 'QC'],
      report: {
        category: '생산',
        date: this.$moment().format('YYYY-MM-DD'),
        prevs: [
          {
            title: '',
            content: '',
            progress: 0
          }
        ],
        nexts: [
          {
            title: '',
            content: '',
            progress: 0
          }
        ]
      },
      edit: false
    }
  },
  watch: {
    'report.category' (n, o) {
      if (n === o) return
      this.read()
    },
    'report.date' (n, o) {
      if (n === o) return
      this.read()
    }
  },
  mounted () {
    this.read()
  },
  methods: {
    async read () {
      const r = await this.$firebase.firestore().collection('reportDays')
        .doc(this.report.category + ' ' + this.report.date)
        .get()
      if (r.exists) {
        this.report = r.data()
        return
      }
      this.report.prevs = [
        {
          title: '',
          content: '',
          progress: 0
        }
      ]
      this.report.nexts = [
        {
          title: '',
          content: '',
          progress: 0
        }
      ]
    }
  }
}
</script>
