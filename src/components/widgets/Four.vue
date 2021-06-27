<template>
	<div class="steps">
		<h2>Step count for the last 7 days</h2>
		<div class="steps-bar-chart">
			<svg ref="barChart" class="bar-chart-svg" xmlns="http://www.w3.org/2000/svg"></svg>
		</div>
	</div>
</template>

<script>
	import activityData from "../../data/activity-data.json";
	export default {
		name: 'Four',
		data() {
			return {
				stepsData: []
			}
		},
		methods: {
			renderChart() {
				const offsetBottom = 5;
				const chartHeight = 100;
				const barColor = "#0586b8";
				const lineColor = "#cfcfcf";
				const barChartContainer = this.$refs.barChart;
				const days = ["Sun", "Mon", "Tues", "Wed", "Thur", "Fri", "Sat"];
				barChartContainer.setAttribute('viewBox', '0 0 100 100');
				
				// TODO: y-axis
				// Draw lines behind the chart.
				// for (let i = 0; i < 11; i++) {
				// 	const line = document.createElementNS("http://www.w3.org/2000/svg", "line");
				// 	line.setAttribute('y1', (i * chartHeight/10) - offsetBottom);
				// 	line.setAttribute('y2', (i * chartHeight/10) - offsetBottom);
				// 	line.setAttribute('x1', 1000);
				// 	line.setAttribute('stroke', lineColor);
				// 	line.setAttribute('stroke-width', '.25px');
				// 	barChartContainer.appendChild(line);
				// }

				const line = document.createElementNS("http://www.w3.org/2000/svg", "line");
				line.setAttribute('y1', (chartHeight) - offsetBottom);
				line.setAttribute('y2', (chartHeight) - offsetBottom);
				line.setAttribute('x1', 1000);
				line.setAttribute('stroke', lineColor);
				line.setAttribute('stroke-width', '.25px');
				barChartContainer.appendChild(line);

				// Draw bars.
				const d = new Date();
				let today = d.getDay();
				for (let i = 0; i < 7; i++) {
					const positionX = i;
					const barHeight = this.stepsData[i] / 120;
					const bar = document.createElementNS("http://www.w3.org/2000/svg", "rect");
					bar.setAttribute('x', positionX * 15);
					bar.setAttribute('y', (chartHeight - barHeight - offsetBottom));
					bar.setAttribute('width', 10);
					bar.setAttribute('height', barHeight);
					bar.setAttribute('fill', barColor);
					barChartContainer.appendChild(bar);

					// Labels.
					// X-axis label.
					const labelX = document.createElementNS("http://www.w3.org/2000/svg", "text");
					labelX.setAttribute('x', positionX * 15 + 5);
					labelX.setAttribute('y', chartHeight);
					labelX.setAttribute('font-size', '3px');
					labelX.setAttribute('text-anchor', 'middle');

					let dayLabel;
					if (today == 6) {
						dayLabel = days[today];
					} else {
						dayLabel = days[today+1];
					}
					today++;
					const textNode = document.createTextNode(dayLabel);
					labelX.appendChild(textNode);

					// Bar label.
					const labelBar = document.createElementNS("http://www.w3.org/2000/svg", "text");
					labelBar.setAttribute('x', positionX * 15 + 5);
					labelBar.setAttribute('y', (chartHeight - barHeight));
					labelBar.setAttribute('font-size', '3px');
					labelBar.setAttribute('fill', 'white');
					labelBar.setAttribute('text-anchor', 'middle');
					const textNodeBar = document.createTextNode(this.stepsData[i]);
					labelBar.appendChild(textNodeBar);

					
					barChartContainer.appendChild(labelX);
					barChartContainer.appendChild(labelBar);
				}				
			}
		},
		mounted() {
			for (const activity of activityData) {
				this.stepsData.push(activity.steps);
			}
			this.renderChart();
		},
	}

</script>

<style type="text/css">
	.bar-chart-svg {
		display: block;
		margin:  auto;
		max-height: 400px;
		max-width: 400px;
	}

	.steps-bar-chart {
		padding: 0 1rem;
	}
</style>