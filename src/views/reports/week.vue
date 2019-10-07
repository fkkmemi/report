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
          <v-col cols="12" sm="6">
            <v-card>
              <v-subheader>지난주</v-subheader>
              <v-divider></v-divider>
              <template three-line v-for="(item, i) in report.prevs">
                <v-list-item :key="i">
                  <v-list-item-content>
                    <v-list-item-title>
                      {{ item.title }}
                    </v-list-item-title>
                    <v-list-item-subtitle>
                      {{ item.content }}
                    </v-list-item-subtitle>
                  </v-list-item-content>
                  <v-list-item-icon>
                    <v-progress-circular
                      :rotate="270"
                      :size="50"
                      :width="10"
                      :value="item.progress"
                      color="pink"
                    >
                      {{ item.progress }}
                    </v-progress-circular>
                  </v-list-item-icon>
                </v-list-item>
                <v-divider :key="i+1000000"></v-divider>
              </template>
            </v-card>
          </v-col>
          <v-col cols="12" sm="6">
            <v-card>
              <v-subheader>다음주</v-subheader>
              <v-divider></v-divider>
              <template three-line v-for="(item, i) in report.nexts">
                <v-list-item :key="i">
                  <v-list-item-content>
                    <v-list-item-title>
                      {{ item.title }}
                    </v-list-item-title>
                    <v-list-item-subtitle>
                      {{ item.content }}
                    </v-list-item-subtitle>
                  </v-list-item-content>
                  <v-list-item-icon>
                    <v-progress-circular
                      :rotate="270"
                      :size="50"
                      :width="10"
                      :value="item.progress"
                      color="pink"
                    >
                      {{ item.progress }}
                    </v-progress-circular>
                  </v-list-item-icon>
                </v-list-item>
                <v-divider :key="i+1000000"></v-divider>
              </template>
            </v-card>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" sm="6">
            <v-card>
              <v-subheader>지난주</v-subheader>
              <template v-for="(item, i) in report.prevs">
                <v-card-text :key="i">
                  <v-text-field v-model="item.title" label="title"></v-text-field>
                  <v-textarea v-model="item.content" label="content"></v-textarea>
                  <v-slider v-model="item.progress" label="progress"></v-slider>
                </v-card-text>
                <v-divider :key="i+1000000"></v-divider>
              </template>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn icon @click="add('prev')">
                  <v-icon>mdi-file-plus-outline</v-icon>
                </v-btn>

              </v-card-actions>
            </v-card>
          </v-col>
          <v-col cols="12" sm="6">
            <v-card>
              <v-subheader>다음주</v-subheader>
              <template v-for="(item, i) in report.nexts">
                <v-card-text :key="i">
                  <v-text-field v-model="item.title" label="title"></v-text-field>
                  <v-textarea v-model="item.content" label="content"></v-textarea>
                  <v-slider v-model="item.progress" label="progress"></v-slider>
                </v-card-text>
                <v-divider :key="i+1000000"></v-divider>
              </template>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn icon @click="add('next')">
                  <v-icon>mdi-file-plus-outline</v-icon>
                </v-btn>

              </v-card-actions>
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
      categoryItems: ['연구소', '생산', 'QC'],
      report: {
        category: this.category,
        date: this.date,
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
      }
    }
  },
  methods: {
    add (type) {
      let job
      if (type === 'prev') job = this.report.prevs
      else job = this.report.nexts
      job.push(
        {
          title: '',
          content: '',
          progress: 0
        }
      )
    }
  }
}
</script>
