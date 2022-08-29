<template>
  <div class="container">
    <h1>All Time</h1>
    <line-chart :dataPoints="chartData" />
    <h1>Results</h1>
    <table>
      <tr>
        <th>Test Title</th>
        <th>Run Date</th>
        <th>Total Time</th>
      </tr>
      <tr v-for="dataPoint in chartData" :key="dataPoint.test">
        <td>{{ dataPoint.test }}</td>
        <td>{{ dataPoint.date.toDateString().toUpperCase() }}</td>
        <td>{{ `${dataPoint.time} ms` }}</td>
      </tr>
    </table>
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
          test: 'Recognition Details',
          date: new Date('2022-01-01'),
          time: 3000,
        },
        {
          test: 'Recognition Details',
          date: new Date('2022-03-03'),
          time: 1000,
        },
        {
          test: 'Recognition Details',
          date: new Date('2022-04-09'),
          time: 2367,
        },
        {
          test: 'Recognition Details',
          date: new Date('2022-06-12'),
          time: 4098,
        },
        {
          test: 'Recognition Details',
          date: new Date('2022-07-16'),
          time: 2098,
        },
        {
          test: 'Recognition Details',
          date: new Date('2022-11-20'),
          time: 3002,
        },
        {
          test: 'Recognition Details',
          date: new Date('2022-12-01'),
          time: 6000,
        },
        {
          test: 'Recognition Details',
          date: new Date('2022-12-20'),
          time: 8000,
        },
        {
          test: 'Points Redeemed',
          date: new Date('2022-01-01'),
          time: 1000,
        },
        {
          test: 'Points Redeemed',
          date: new Date('2022-03-21'),
          time: 800,
        },
        {
          test: 'Points Redeemed',
          date: new Date('2022-04-01'),
          time: 2000,
        },
        {
          test: 'Points Redeemed',
          date: new Date('2022-07-12'),
          time: 3209,
        },
        {
          test: 'Points Redeemed',
          date: new Date('2022-07-30'),
          time: 1999,
        },
        {
          test: 'Points Redeemed',
          date: new Date('2022-11-11'),
          time: 2831,
        },
        {
          test: 'Points Redeemed',
          date: new Date('2022-12-11'),
          time: 4000,
        },
        {
          test: 'Points Redeemed',
          date: new Date('2022-12-30'),
          time: 2000,
        },
      ],
    }
  },
}
</script>

<style>
body {
  display: flex;
  justify-content: center;
  font-family: 'Poppins';
}
h1 {
  font-size: 24px;
}
.container {
  width: 50vw;
  padding: 24px;
  background-color: white;
}
table {
  width: 100%;
}
table,
td,
th {
  border: 1px solid #e9eaec;
  border-collapse: collapse;
}
td,
th {
  padding: 8px 16px;
}
th {
  background-color: #eff2f5;
  font-size: 14px;
}
td {
  background-color: #f4f6fc;
  font-size: 12px;
  font-family: 'JetBrains Mono';
}
</style>
