<template>
  <div>
    <h1 class="display-1 mt-3 mb-5">
      {{ shop.name }}
    </h1>
    <v-row>
      <v-col cols="12" md="6">
        <v-alert
          v-if="url"
          dark
          color="accent"
          elevation="2"
        >
          {{ $t('misc.shop_url') }} <a :href="url" target="_blank">{{ url }}</a>
        </v-alert>
      </v-col>
    </v-row>
    <v-card class="pt-1 mt-5">
      <v-card-title>
        {{ $t("titles.transactions") }}
        <v-spacer />
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          :label="$t('fields.search')"
          single-line
          hide-details
        />
      </v-card-title>
      <v-data-table
        item-key="code"
        :headers="headers"
        :items="transactions"
        :search="search"
      />
    </v-card>
  </div>
</template>
<script>

export default {
  name: 'ShopIndex',
  props: {
    shop: {
      type: Object,
      required: true
    },
    url: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      search: '',
      headers: [
        { text: 'Id', value: 'id' },
        { text: 'Kupujący', value: 'nick' },
        { text: 'Brama', value: 'type' }
      ]
    }
  },
  head () {
    return {
      title: this.$t('titles.dashboard')
    }
  },
  computed: {
    transactions () {
      const result = []
      for (const i in this.shop.history) {
        result.push({
          id: i,
          nick: this.shop.history[i].nick,
          type: this.shop.history[i].type
        })
      }
      return result
    }
  }
}
</script>
