<template>
  <section class="section">
    <div class="columns is-mobile">
      <card title="Free" icon="github">
        Open source on <a href="https://github.com/buefy/buefy"> GitHub </a>
      </card>

      <card title="Responsive" icon="cellphone-link">
        <b class="has-text-grey"> Every </b> component is responsive
      </card>

      <card title="Modern" icon="alert-decagram">
        Built with <a href="https://vuejs.org/"> Vue.js </a> and
        <a href="http://bulma.io/"> Bulma </a>
      </card>

      <card title="Lightweight" icon="arrange-bring-to-front">
        No other internal dependency
      </card>
      <button @click="api">
        api
      </button>
    </div>
  </section>
</template>

<script>
import Card from '~/components/Card'

export default {
  name: 'HomePage',

  components: {
    Card
  },
  methods: {
    test () {
      console.log('test')
    },
    async api () {
      const Snoowrap = require('snoowrap')

      // NOTE: The following examples illustrate how to use snoowrap. However, hardcoding
      // credentials directly into your source code is generally a bad idea in practice (especially
      // if you're also making your source code public). Instead, it's better to either (a) use a separate
      // config file that isn't committed into version control, or (b) use environment variables.

      // Create a new snoowrap requester with OAuth credentials.
      // For more information on getting credentials, see here: https://github.com/not-an-aardvark/reddit-oauth-helper
      // Alternatively, just pass in a username and password for script-type apps.
      const r = new Snoowrap({
        userAgent: 'Nuxt App:1:1.0 (by /u/thebliterator)',
        clientId: 'ID4umaeS_clyYA',
        clientSecret: '4J3b1w9CmDheko7jmWZRF0r0AOiHDg',
        username: `${this.$config.username}`,
        password: `${this.$config.password}`
      })
      const subreddit = await r.getSubreddit('stocks')
      const search = await subreddit.search({ query: 'gme', sort: 'year' })
      console.log(search)
    }
  }
}
</script>
