<template>
  <div>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.1.2/dist/tailwind.min.css" rel="stylesheet">
    <!-- <Header @closeDetail="toggleView" /> -->
    <transition-group mode="in-out">
      <Arrow v-show="!detailView" :key="1" :stocks=stocks @shareSelected="toggleView" />
      <DetailView v-show="detailView" :key="2" :stocks=stocks @closeDetail="toggleView" />
    </transition-group>
  </div>
</template>

<script>
function loadData(query, apiVersion, url) {
  return new Promise((resolve, reject) => {
    const qlCommand = {
      operationName: "EODTimeseries",
      query: query,
    };

    let headers = {
      Accept: "application/json",
      "Content-Type": "application/json",
      "api-version": apiVersion,
    };

    console.log("COMMAND: ", qlCommand);

    fetch(url, {
      method: "post",
      headers: headers,
      body: JSON.stringify(qlCommand),
    })
      .then((response) => response.json())
      .then((data) => {
        resolve(data);
      })
      .catch(reject);
  });
}
module.exports = {
  data: function () {
    return {
      detailView: false,
      tickers: ["NFLX_67", "TSLA_67", "AAPL_67", "ABNB_67", "AMZN_67", "SCMN_4","SREN_4","HOLNE_4","CSGN_4","ROG_4","LOGN_4","NESN_4"],
      stocks: [],
    };
  },
  methods: {
    toggleView() {
      console.log("changeView");
      this.detailView = !this.detailView;
    },
    fetchTimeseries() {
      let url = "https://web.api.six-group.com/api/findata/v1/graphql";

      let apiVersion = "2022-01-01";

      // start first trading day of the year
      let startDay = "2023-01-03";

      const graphQLQuery = `query EODTimeseries {
        listings(scheme: TICKER_BC, ids: ["${this.tickers.join('","')}"]) {
          requestedId
          requestedScheme
          lookupStatus
          lookup {
            listingName
            marketName
            listingCurrency
            listingStatus
          }
          marketData {
              eodTimeseries(filters: {from: "${startDay}"}) {
                sessionDate
                open
                close
                low
                high
                volume
                yieldToMaturity
                turnover
                netAssetValue
                settlementPrice
                openInterest
                vwap
              }
           }
        }
      }`;

      loadData(graphQLQuery, apiVersion, url).then((res) => {
        console.log("data loaded", res);
        let listings = res.data?.listings;

        let result = [];

        listings.forEach((listing) => {
          console.log(listing);
          let ytdTrend = null;
          try {
            ytdTrend =
              (100 / listing.marketData.eodTimeseries[0].close) *
                listing.marketData.eodTimeseries[
                  listing.marketData.eodTimeseries.length - 1
                ].open -
              100;
          } catch (err) {
            console.log("YTD Trend not calculated", err);
          }

          result.push({
            name: listing.lookup.listingName,
            trendYTD: ytdTrend,
            trend7: 0,
          });
        });
        console.log(result);
        this.stocks = result;
      });
    },
  },
  mounted() {
    this.fetchTimeseries();
  },
};
</script>

<style>
body {
  padding: 0;
  margin: 0;
  background: white;
}
/* .slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: none;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
} */
.v-enter-active {
  transition: all 0.5s ease;
}

.v-enter-from {
  transform: translateY(100vh);
  opacity: 0;
}
</style>
