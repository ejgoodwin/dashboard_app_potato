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
				const chartHeight = 100;
				const charWidth = 150;
				const offsetBottom = 5;
				let scale = 100;
				let dataPeak = 0;

				const barChartContainer = this.$refs.barChart;	
				const barGap = 6;
				const barWidth = charWidth/this.stepsData.length - barGap;
				const barStartPosition = charWidth/this.stepsData.length - 2;
				const barLabelPositionOffset = barWidth/2;

				const barColor = "#0586b8";
				const barColorTarget = "#05b3b8"
				const lineColor = "#cfcfcf";
				const tenThousandColour = "#068b71";
				const fiveThousandColour = "#a6a6a6";
				const days = ["Sun", "Mon", "Tues", "Wed", "Thur", "Fri", "Sat"];
				let tenThousandLine = 0;
				let fiveThousandLine = 0;
				
				barChartContainer.setAttribute('viewBox', `0 0 ${charWidth} ${chartHeight}`);

				// Find highest count in data.
				this.stepsData.forEach((day) => {
					if (day > dataPeak) {
						dataPeak = day;
					}
				});

				// Round peak to nearest 1000 and use it to scale the chart.
				dataPeak = Math.ceil(dataPeak/1000)*1000;
				scale = dataPeak/100;
				tenThousandLine = 100 - (10000/scale);
				fiveThousandLine = 100 - (5000/scale);
				
				// Line for 10,000 mark.
				const topLine = document.createElementNS("http://www.w3.org/2000/svg", "line");
				topLine.setAttribute('y1', tenThousandLine);
				topLine.setAttribute('y2', tenThousandLine);
				topLine.setAttribute('x1', charWidth);
				topLine.setAttribute('stroke-dasharray', '1,1');
				topLine.setAttribute('stroke', tenThousandColour);
				topLine.setAttribute('stroke-width', '.25px');
				barChartContainer.appendChild(topLine);

				// Text for 10,000 mark.
				const topLineText = document.createElementNS("http://www.w3.org/2000/svg", "text");
				topLineText.setAttribute('x', charWidth - 9);
				topLineText.setAttribute('y', tenThousandLine - 2);
				topLineText.setAttribute('font-size', '3px');
				topLineText.setAttribute('fill', tenThousandColour);
				const topLineTextNode = document.createTextNode('10,000');
				topLineText.appendChild(topLineTextNode);
				barChartContainer.appendChild(topLineText);

				// Line for 5,000 mark.
				const middleLine = document.createElementNS("http://www.w3.org/2000/svg", "line");
				middleLine.setAttribute('y1', fiveThousandLine);
				middleLine.setAttribute('y2', fiveThousandLine);
				middleLine.setAttribute('x1', charWidth);
				middleLine.setAttribute('stroke-dasharray', '1,1');
				middleLine.setAttribute('stroke', fiveThousandColour);
				middleLine.setAttribute('stroke-width', '.25px');
				barChartContainer.appendChild(middleLine);

				// Text for 5,000 mark.
				const middleLineText = document.createElementNS("http://www.w3.org/2000/svg", "text");
				middleLineText.setAttribute('x', charWidth - 8);
				middleLineText.setAttribute('y', fiveThousandLine - 2);
				middleLineText.setAttribute('font-size', '3px');
				middleLineText.setAttribute('fill', fiveThousandColour);
				const middleLineTextNode = document.createTextNode('5,000');
				middleLineText.appendChild(middleLineTextNode);
				barChartContainer.appendChild(middleLineText);

				// Line for x-axis.
				const line = document.createElementNS("http://www.w3.org/2000/svg", "line");
				line.setAttribute('y1', chartHeight - offsetBottom);
				line.setAttribute('y2', chartHeight - offsetBottom);
				line.setAttribute('x1', charWidth);
				line.setAttribute('stroke', lineColor);
				line.setAttribute('stroke-width', '.25px');
				barChartContainer.appendChild(line);

				// Draw bars.
				const d = new Date();
				let today = d.getDay();
				let positionX = 0;
				for (let i = 0; i < 7; i++) {
					
					const barHeight = this.stepsData[i] / scale - offsetBottom;
					const bar = document.createElementNS("http://www.w3.org/2000/svg", "rect");
					bar.setAttribute('x', positionX);
					bar.setAttribute('y', (chartHeight - barHeight - offsetBottom));
					bar.setAttribute('width', barWidth);
					bar.setAttribute('height', barHeight);
					if (this.stepsData[i] >= 10000) {
						bar.setAttribute('fill', barColorTarget);
					} else {
						bar.setAttribute('fill', barColor);
					}
					
					barChartContainer.appendChild(bar);
					// Labels.
					// X-axis label.
					const labelX = document.createElementNS("http://www.w3.org/2000/svg", "text");
					labelX.setAttribute('x', positionX + barLabelPositionOffset);
					labelX.setAttribute('y', chartHeight);
					labelX.setAttribute('font-size', '3px');
					labelX.setAttribute('text-anchor', 'middle');
					
					let dayLabel;
					console.log(today);
					dayLabel = days[today];
					if (today == 6) {
						today = 0;
					} else {
						today++;
					}
					
					const textNode = document.createTextNode(dayLabel);
					labelX.appendChild(textNode);

					// Bar label.
					const labelBar = document.createElementNS("http://www.w3.org/2000/svg", "text");
					labelBar.setAttribute('x', positionX + barLabelPositionOffset);
					labelBar.setAttribute('y', (chartHeight - barHeight));
					labelBar.setAttribute('font-size', '3px');
					labelBar.setAttribute('fill', 'white');
					labelBar.setAttribute('text-anchor', 'middle');
					const textNodeBar = document.createTextNode(this.stepsData[i]);
					labelBar.appendChild(textNodeBar);
					
					barChartContainer.appendChild(labelX);
					barChartContainer.appendChild(labelBar);

					positionX += barStartPosition;
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