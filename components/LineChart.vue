<template>
  <div>
    <svg class="chart" />
    <div
      v-if="tooltipData && tooltipPositioning"
      class="dot-tooltip"
      :style="`left: ${tooltipPositioning.x + 12}px; top: ${
        tooltipPositioning.y + 12
      }px;`"
    >
      <h3>Run Date</h3>
      <p>{{ tooltipData.date.toDateString() }}</p>
      <h3>Total Time</h3>
      <p>{{ tooltipData.time }}</p>
    </div>
  </div>
</template>

<script>
import * as d3 from 'd3'

export default {
  name: 'line-chart',
  props: {
    dataPoints: {
      required: true,
      type: Array,
    },
    tooltipData: {
      required: false,
      type: Object,
    },
    tooltipPositioning: {
      required: false,
      type: Object,
    },
  },
  methods: {
    // Copyright 2021 Observable, Inc.
    // Released under the ISC license.
    // https://observablehq.com/@d3/line-chart
    drawChart(
      data,
      {
        x = ([x]) => x, // given d in data, returns the (temporal) x-value
        y = ([, y]) => y, // given d in data, returns the (quantitative) y-value
        defined, // for gaps in data
        curve = d3.curveLinear, // method of interpolation between points
        marginTop = 20, // top margin, in pixels
        marginRight = 30, // right margin, in pixels
        marginBottom = 30, // bottom margin, in pixels
        marginLeft = 40, // left margin, in pixels
        width = 640, // outer width, in pixels
        height = 256, // outer height, in pixels
        xType = d3.scaleTime, // the x-scale type
        xDomain = [new Date('2022-01-01'), new Date('2022-12-31')], // [xmin, xmax]
        xRange = [marginLeft, width - marginRight], // [left, right]
        yType = d3.scaleLinear, // the y-scale type
        yDomain, // [ymin, ymax]
        yRange = [height - marginBottom, marginTop], // [bottom, top]
        yFormat, // a format specifier string for the y-axis
        yLabel, // a label for the y-axis
        color = 'red', // stroke color of line
        strokeLinecap = 'round', // stroke line cap of the line
        strokeLinejoin = 'round', // stroke line join of the line
        strokeWidth = 2, // stroke width of line, in pixels
        strokeOpacity = 1, // stroke opacity of line
      } = {}
    ) {
      const addTooltipProperties = (event, d) => {
        this.tooltipData = { date: d.date, time: d.time }
        this.tooltipPositioning = { x: event.x, y: event.y }
      }

      const resetTooltipProperties = () => {
        this.tooltipData = null
        this.tooltipPositioning = null
      }

      // Compute values.
      const X = d3.map(data, x)
      const Y = d3.map(data, y)
      const I = d3.range(X.length)
      if (defined === undefined)
        defined = (d, i) => !isNaN(X[i]) && !isNaN(Y[i])
      const D = d3.map(data, defined)

      // Compute default domains.
      if (xDomain === undefined) xDomain = d3.extent(X)
      if (yDomain === undefined) yDomain = d3.extent(Y)

      // Construct scales and axes.
      const xScale = xType(xDomain, xRange)
      const yScale = yType(yDomain, yRange)
      const xAxis = d3.axisBottom(xScale)
      const yAxis = d3.axisLeft(yScale)

      // Customize axis ticks
      xAxis.tickSize(-(height - marginTop - marginBottom))
      xAxis.tickPadding(12)
      xAxis.tickFormat(d3.timeFormat('%b')) // February -> Feb

      yAxis.tickSizeInner(-(width - marginLeft - marginRight))
      yAxis.tickSizeOuter(0)
      yAxis.tickPadding(12)
      yAxis.tickFormat(d3.format('~s')) // 1,000 -> 1K
      yAxis.ticks(9)

      // Construct a line generator.
      const line = d3
        .line()
        .defined((i) => D[i])
        .curve(curve)
        .x((i) => xScale(X[i]))
        .y((i) => yScale(Y[i]))

      // Define svg element
      const svg = d3
        .select('.chart')
        .attr('width', '100%')
        .attr('height', '50%')
        .attr('viewBox', [0, 0, width, height])
        .attr('style', 'max-width: 100%; height: auto; height: intrinsic;')

      // Define x axis
      svg
        .append('g')
        .attr('transform', `translate(0,${height - marginBottom})`)
        .call(xAxis)
        .call((g) => g.selectAll('.domain').attr('stroke', '#e5e7eb'))
        .call((g) => g.selectAll('.tick line').attr('stroke', '#e5e7eb'))

      // Define y axis
      svg
        .append('g')
        .attr('transform', `translate(${marginLeft},0)`)
        .call(yAxis)
        .call((g) => g.selectAll('.domain').remove())
        .call((g) => g.selectAll('.tick line').attr('stroke', '#e5e7eb'))
        .attr('stroke-dasharray', '5,5')

      // Plot line
      svg
        .append('path')
        .attr('fill', 'none')
        .attr('stroke', color)
        .attr('stroke-width', strokeWidth)
        .attr('stroke-linecap', strokeLinecap)
        .attr('stroke-linejoin', strokeLinejoin)
        .attr('stroke-opacity', strokeOpacity)
        .attr('d', line(I))

      // Plot dots
      svg
        .selectAll('dot')
        .data(data)
        .enter()
        .append('circle')
        .attr('class', 'dot')
        .attr('r', 4)
        .attr('cx', function (d) {
          return xScale(d.date)
        })
        .attr('cy', function (d) {
          return yScale(d.time)
        })
        .attr('stroke', '#20C4F4')
        .attr('stroke-width', 2)
        .style('fill', 'white')
        .on('mouseover', function (event, d) {
          d3.select(this).transition().duration(100).attr('r', 8)
          addTooltipProperties(event, d)
        })
        .on('mouseout', function () {
          d3.select(this).transition().duration(100).attr('r', 4)
          resetTooltipProperties()
        })

      return svg.node()
    },
    renderChart(dataPoints) {
      this.drawChart(dataPoints, {
        x: (d) => d.date,
        y: (d) => d.time,
        color: '#20C4F4',
      })
    },
  },
  mounted() {
    this.renderChart(this.dataPoints)
  },
}
</script>

<style>
text {
  font-size: 14;
  font-family: 'JetBrains Mono', monospace;
  text-transform: uppercase;
}
.dot-tooltip {
  position: absolute;
  z-index: 1000;
  background-color: #eff1f8;
  border: 1px solid #dae0ea;
  border-radius: 8px;
  padding: 12px;
  font-family: 'JetBrains Mono', monospace;
  box-shadow: 0 2px 4px rgb(105 112 117 / 15%);
}
.dot-tooltip > h3 {
  font-size: 14;
}
.dot-tooltip > p {
  font-size: 12;
}
</style>