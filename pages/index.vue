<template>
  <div class="container">
    <h1>Test Results</h1>
    <line-graph :data="chartData" />
    <div>Table</div>
  </div>
</template>

<script>
import LineGraph from '../components/LineGraph'

export default {
  name: 'IndexPage',
  components: {
    LineGraph,
  },
  data() {
    return {
      chartData: [
        {
          date: new Date('2022-01-01'),
          time: 3000,
        },
        {
          date: new Date('2022-03-03'),
          time: 1000,
        },
        {
          date: new Date('2022-04-09'),
          time: 2367,
        },
        {
          date: new Date('2022-06-12'),
          time: 4098,
        },
        {
          date: new Date('2022-07-16'),
          time: 2098,
        },
        {
          date: new Date('2022-11-20'),
          time: 3002,
        },
        {
          date: new Date('2022-12-01'),
          time: 6000,
        },
        {
          date: new Date('2022-12-20'),
          time: 8000,
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
}
.container {
  width: 66vw;
  padding: 24px;
  background-color: white;
}
</style>
