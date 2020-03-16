<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <v-flex
      xs12
      sm8
      md6
    >
      <v-sheet v-if="items">
        <v-btn class="mb-4" @click="test">
          microCMS取得ConsoleLog
        </v-btn>
        <v-card v-for="(x, i) in items" :key="i" class="mb-4">
          <v-img
            class="white--text align-end"
            height="200px"
            :src="x.newsImage.url"
          >
            <v-card-title>
              {{ x.title }}
            </v-card-title>
          </v-img>
          <v-card-subtitle class="pb-0">
            {{ x.publishedAt }}
          </v-card-subtitle>
          <v-card-text class="text--primary">
            {{ x.body }}
          </v-card-text>
        </v-card>
      </v-sheet>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      items: []
    }
  },
  async asyncData () {
    const { data } = await axios.get(
      'https://icen.microcms.io/api/v1/news',
      {
        headers: { 'X-API-KEY': process.env.API_KEY }
      }
    )
    return {
      items: data.contents
    }
  },
  methods: {
    test () {
      console.log(this.items)
    }
  },
  components: {
  }
}
</script>
