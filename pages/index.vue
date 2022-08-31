<template>
  <div class="container">
    <h1>All Time</h1>
    <line-chart :dataPoints="chartData" />
    <check-box
      v-for="group in lineGroups"
      :key="group"
      :id="group"
      checked="false"
      :label="group"
      style="margin-bottom: 4px"
      :value="group"
    />
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
import CheckBox from '../components/CheckBox'

export default {
  name: 'IndexPage',
  components: {
    LineChart,
    CheckBox,
  },
  data() {
    return {
      chartData: [
        {
          id: 1,
          test: 'Recognition Details',
          date: new Date('2022-01-01'),
          time: 3000,
        },
        {
          id: 2,
          test: 'Recognition Details',
          date: new Date('2022-03-03'),
          time: 1000,
        },
        {
          id: 3,
          test: 'Recognition Details',
          date: new Date('2022-04-09'),
          time: 2367,
        },
        {
          id: 4,
          test: 'Recognition Details',
          date: new Date('2022-06-12'),
          time: 4098,
        },
        {
          id: 5,
          test: 'Recognition Details',
          date: new Date('2022-07-16'),
          time: 2098,
        },
        {
          id: 6,
          test: 'Recognition Details',
          date: new Date('2022-11-20'),
          time: 3002,
        },
        {
          id: 7,
          test: 'Recognition Details',
          date: new Date('2022-12-01'),
          time: 6000,
        },
        {
          id: 8,
          test: 'Recognition Details',
          date: new Date('2022-12-20'),
          time: 8000,
        },
        {
          id: 9,
          test: 'Points Redeemed',
          date: new Date('2022-01-01'),
          time: 1000,
        },
        {
          id: 10,
          test: 'Points Redeemed',
          date: new Date('2022-03-21'),
          time: 800,
        },
        {
          id: 11,
          test: 'Points Redeemed',
          date: new Date('2022-04-01'),
          time: 2000,
        },
        {
          id: 12,
          test: 'Points Redeemed',
          date: new Date('2022-07-12'),
          time: 3209,
        },
        {
          id: 13,
          test: 'Points Redeemed',
          date: new Date('2022-07-30'),
          time: 1999,
        },
        {
          id: 14,
          test: 'Points Redeemed',
          date: new Date('2022-11-11'),
          time: 2831,
        },
        {
          id: 15,
          test: 'Points Redeemed',
          date: new Date('2022-12-11'),
          time: 4000,
        },
        {
          id: 16,
          test: 'Points Redeemed',
          date: new Date('2022-12-30'),
          time: 2000,
        },
      ],
    }
  },
  computed: {
    lineGroups() {
      let groups = new Set()
      this.chartData.forEach((dataPoint) => {
        groups.add(dataPoint.test)
      })

      return groups
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
