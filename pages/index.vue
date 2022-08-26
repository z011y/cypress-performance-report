<template>
  <div class="container">
    <h1>All Time</h1>
    <line-chart :dataPoints="chartData" />
    <h1>Results</h1>
    <div class="results-table">
      <div class="results-table-header">Test Title</div>
      <div class="results-table-header">Run Date</div>
      <div class="results-table-header">Total Time (ms)</div>
      <div
        class="results-table-row"
        v-for="dataPoint in flattenedData()"
        :key="dataPoint"
      >
        {{
          typeof dataPoint === 'object' ? dataPoint.toDateString() : dataPoint
        }}
      </div>
    </div>
  </div>
</template>

<script>
import LineChart from '../components/LineChart'

export default {
  name: 'IndexPage',
  components: {
    LineChart,
  },
  data() {
    return {
      chartData: [
        {
          test: 'Recognition Details Report',
          date: new Date('2022-01-01'),
          time: 3000,
        },
        {
          test: 'Recognition Details Report',
          date: new Date('2022-03-03'),
          time: 1000,
        },
        {
          test: 'Recognition Details Report',
          date: new Date('2022-04-09'),
          time: 2367,
        },
        {
          test: 'Recognition Details Report',
          date: new Date('2022-06-12'),
          time: 4098,
        },
        {
          test: 'Recognition Details Report',
          date: new Date('2022-07-16'),
          time: 2098,
        },
        {
          test: 'Recognition Details Report',
          date: new Date('2022-11-20'),
          time: 3002,
        },
        {
          test: 'Recognition Details Report',
          date: new Date('2022-12-01'),
          time: 6000,
        },
        {
          test: 'Recognition Details Report',
          date: new Date('2022-12-20'),
          time: 8000,
        },
        {
          test: 'Points Redeemed Report',
          date: new Date('2022-01-01'),
          time: 1000,
        },
        {
          test: 'Points Redeemed Report',
          date: new Date('2022-03-21'),
          time: 800,
        },
        {
          test: 'Points Redeemed Report',
          date: new Date('2022-04-01'),
          time: 2000,
        },
        {
          test: 'Points Redeemed Report',
          date: new Date('2022-07-12'),
          time: 3209,
        },
        {
          test: 'Points Redeemed Report',
          date: new Date('2022-07-30'),
          time: 1999,
        },
        {
          test: 'Points Redeemed Report',
          date: new Date('2022-11-11'),
          time: 2831,
        },
        {
          test: 'Points Redeemed Report',
          date: new Date('2022-12-11'),
          time: 4000,
        },
        {
          test: 'Points Redeemed Report',
          date: new Date('2022-12-30'),
          time: 2000,
        },
      ],
    }
  },
  methods: {
    flattenedData() {
      return this.chartData
        .map((data) => {
          return Object.values(data)
        })
        .flat()
    },
  },
}
</script>

<style>
body {
  display: flex;
  justify-content: center;
  font-family: 'Poppins';
}
.container {
  width: 50vw;
  padding: 24px;
  background-color: white;
}
.results-table {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  background-color: #dae0ea;
  width: 100%;
  border-radius: 12px;
  grid-gap: 1px;
  border: 1px solid #dae0ea;
  overflow: hidden;
}
.results-table-header {
  display: flex;
  align-items: center;
  height: 48px;
  padding-left: 12px;
  background-color: #eff1f8;
  font-weight: 700;
}
.results-table-row {
  display: flex;
  align-items: center;
  height: 48px;
  padding-left: 12px;
  background-color: #f4f6fc;
  font-size: 12px;
}
</style>
