<template>
 <v-card class="transparent ma-5 pa-1 elevation-0">
  <v-form v-model="valid0" ref="form" lazy-validation>
    <v-text-field
      label="Key: Artist"
      v-model="artist">
    </v-text-field>
    <v-text-field
      label="Key: Song Title"
      v-model="songtitle">
    </v-text-field>
    <v-btn @click.native="deleteitem()">Submit</v-btn>
  </v-form>
</v-card>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      artist: '',
      songtitle: '',
      valid0: false
    }
  },
  methods: {
    deleteitem: function () {
      let payload = {
        Key: {
          Artist: {
            S: this.artist
          },
          SongTitle: {
            S: this.songtitle
          }
        },
        ReturnConsumedCapacity: 'TOTAL',
        TableName: 'aws-dynamodb-dev-sample-table'
      }

      axios.post('/deleteitem', payload)
        .then(res => {
          console.log('Response:')
          console.log(res)
        })
        .catch(err => {
          console.log('Error:')
          console.log(err)
        })
    }
  }
}
</script>
<style scoped>
</style>
