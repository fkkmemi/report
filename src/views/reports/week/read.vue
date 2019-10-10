<template>
  <v-card flat>
    <v-row>
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
  </v-card>
</template>
<script>
export default {
  props: ['report']
}
</script>
