<template>
  <v-card flat>
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
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn @click="write" color="primary">write</v-btn>

    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  props: ['report'],
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
    },
    async write () {
      await this.$firebase.firestore().collection('reportDays')
        .doc(this.report.category + ' ' + this.report.date)
        .set(this.report)
      await this.$firebase.firestore().collection('reportDays')
        .doc('items')
        .update({
          category: this.$firebase.firestore.FieldValue.arrayUnion(this.report.category),
          date: this.$firebase.firestore.FieldValue.arrayUnion(this.report.date)
        })

      this.$emit('editFalse')
    }
  }
}
</script>
