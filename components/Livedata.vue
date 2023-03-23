<!-- Please remove this file from your project -->
<template>
  <div class="grid relative flex items-top min-h-screen bg-gray-100 sm:pt-0">
    <div class="grid grid-cols-3">
      <div class="mt-6 ml-6">
        <p v-if="connection">
          Weboscket state {{ connection.readyState }}
        </p>
        <button @click="sendMessage" class="mt-6 bg-blue-500 rounded py-4 px-4 w-full">Subscribe</button>
        <input class="mt-6 w-full" v-model="ticker" />
        <h2>Message Stream</h2>
        <p v-if="false" v-for="message in messages">
          {{ message.data }}
        </p>
      </div>
      <div>
        <p v-if="tickerValue" class="m-8 text-lg">
          Kurs: <span :class="textColor">{{ tickerValue }}</span>
        </p>
      </div>
    </div>

  </div>
</template>

<script>
import * as stream from "stream";

const WS_URL = 'wss://web.api.six-group.com/api/findata/v1/websocket'
export default {
  name: 'Livedata',
  props: {
    ticker: String
  },
  data: () => ({
    websocketState: '',
    connection: null,
    messages: [],
    tickerValue: null,
    textColor: 'text-black-400',
    streamCounter: -1
  }),
  mounted () {
    this.connection = new WebSocket(WS_URL)

    this.connection.onmessage = (event) => {
      console.log(event);
      this.messages.push(event)

      if (event.data) {
        let data = JSON.parse(event.data)
        console.log(data)
        let lastValue = data.data?.startStream[0].last?.value
        console.log(lastValue)
        if (!this.tickerValue) {
          // value is set initially

        } else if (lastValue > this.tickerValue) {
          // value is increased
          this.textColor = 'text-green-400'
        } else if (lastValue < this.tickerValue) {
          // value decreased
          this.textColor = 'text-red-400'
        } else if (lastValue === this.tickerValue) {
          // value stays
          this.textColor = 'text-black-400'
        }

        this.tickerValue = lastValue
      }

      // console.log(event.)
    }

    this.connection.onopen = (event) => {
      console.log(event)
      console.log("Successfully connected to the echo websocket server...")
    }
  },
  methods: {

    sendMessage: function() {
      this.streamCounter += 1
      const query = `subscription { startStream(streamId: "stream_${crypto.randomUUID()}" scheme: TICKER_BC ids: ["${ticker}"]) {
        type requestedId requestedScheme qualityOfService
        last { value timestamp size }
        high { value timestamp }
        low { value timestamp }
        bestBid { value timestamp }
        bestAsk { value timestamp }
        orderBook { position side size value timestamp }
      }}`

      console.log(query)

      const json = JSON.stringify({query: query });
      this.connection.send(json);
    }
  },
}
</script>
