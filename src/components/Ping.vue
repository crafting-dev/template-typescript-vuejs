<template>
  <div class="ping">
    <form @submit.prevent="pingServer">
      <input v-model="ping" placeholder="Ping server with some text...">
      <div class="code-display">
        <code>
          {
            "ping": "{{ ping }}"
          }
        </code>
      </div>

      <button type="submit">Submit</button>
    </form>

    <div v-if="pong">
      <code>
        {{
          JSON.stringify({
            "ping": pong.ping,
            "received_at": new Date(pong.received_at).toLocaleString()
          }, null, 2)
        }}
      </code>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Ping',
  data () {
    return {
      ping: '',
      pong: null
    }
  },
  methods: {
    async pingServer () {
      function createBaseUrl () {
        const locationToMatchRegex = new RegExp('^http://localhost:[0-9]*')
        if (locationToMatchRegex.test(window.location.origin)) {
          // The host:port serving the backend in a two endpoint setup
          return 'http://localhost:3000'
        }
        // The current window URL in a single endpoint setup
        // A /ping path_prefix serves the backend
        return window.location.origin
      }

      const baseUrl = createBaseUrl()
      const response = await fetch(`${baseUrl}/ping?ping=${this.ping}`)
      const data = await response.json()
      this.pong = data
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  width: 300px;
  max-width: 100%;
  height: 30px;
  border-radius: 5px;
  border: 2px solid #373B41;
  padding: 0 20px;
  font-size: 15px;
}
.code-display {
  margin: 20px 0;
}
button {
  margin-bottom: 20px;
  background-color: #373B41;
  border-radius: 5px;
  color: #C5C8C6;
  padding: 5px 40px;
}
</style>
