<template>
	<div class="p-grid p-fluid">
		<div class="p-col-12 p-lg-6">
			<div class="card">
				<h5 class="centerText">Linear Chart</h5>
				<Chart type="line" :data="lineData" />
			</div>

			<div class="card">
				<h5 class="centerText">Pie Chart</h5>
				<Chart type="pie" :data="pieData" />
			</div>

			<div class="card">
				<h5 class="centerText">Polar Area Chart</h5>
				<Chart type="polarArea" :data="polarData" />
			</div>
		</div>
		<div class="p-col-12 p-lg-6">
			<div class="card">
				<h5 class="centerText">Bar Chart</h5>
				<Chart type="bar" :data="barData" />
			</div>

			<div class="card">
				<h5 class="centerText">Doughnut Chart</h5>
				<Chart type="doughnut" :data="pieData" />
			</div>

			<div class="card">
				<h5 class="centerText">Radar Chart</h5>
				<Chart type="radar" :data="radarData" />
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			lineData: {
				labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
				datasets: [
					{
						label: 'First Dataset',
						data: [65, 59, 80, 81, 56, 55, 40],
						fill: false,
						borderColor: '#03A9F4'
					},
					{
						label: 'Second Dataset',
						data: [28, 48, 40, 19, 86, 27, 90],
						fill: false,
						borderColor: '#FFC107'
					}
				]
			},
			pieData: {
				labels: ['A', 'B', 'C'],
				datasets: [
					{
					data: [540, 325, 702, 421],
					backgroundColor: [
						'rgb(54, 162, 235)',
						'rgb(255, 99, 132)',
						'rgb(255, 205, 86)',
						'rgb(75, 192, 192)'
					]
                }]
			},
			polarData: {
				datasets: [{
					data: [
						11,
						16,
						7,
						3
					],
					backgroundColor: [
						'rgb(54, 162, 235)',
						'rgb(255, 99, 132)',
						'rgb(255, 205, 86)',
						'rgb(75, 192, 192)'
					],
					label: 'My dataset'
				}],
				labels: [
					'Blue',
					'Purple',
					'Orange',
					'Green'
				]
			},
			barData: {
				labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
				datasets: [
					{
						label: 'My First dataset',
						backgroundColor: 'rgb(255, 99, 132)',
						borderColor: 'rgb(255, 99, 132)',
						data: [65, 59, 80, 81, 56, 55, 40]
					},
					{
						label: 'My Second dataset',
						backgroundColor: 'rgb(54, 162, 235)',
						borderColor: 'rgb(54, 162, 235)',
						data: [28, 48, 40, 19, 86, 27, 90]
					}
            ]
			},
			doughnutData: {
				labels: ['A','B','C'],
				datasets: [
					{
						data: [300, 50, 100],
						backgroundColor: [
							"#FFC107",
							"#03A9F4",
							"#4CAF50"
						],
						hoverBackgroundColor: [
							"#FFE082",
							"#81D4FA",
							"#A5D6A7"
						]
					}]
			},
			radarData: {
				labels: ['Eating', 'Drinking', 'Sleeping', 'Designing', 'Coding', 'Cycling', 'Running'],
				datasets: [
					{
						label: 'My First dataset',
						backgroundColor: 'rgba(179,181,198,0.2)',
						borderColor: 'rgba(179,181,198,1)',
						pointBackgroundColor: 'rgba(179,181,198,1)',
						pointBorderColor: '#fff',
						pointHoverBackgroundColor: '#fff',
						pointHoverBorderColor: 'rgba(179,181,198,1)',
						data: [65, 59, 90, 81, 56, 55, 40]
					},
					{
						label: 'My Second dataset',
						backgroundColor: 'rgba(255,99,132,0.2)',
						borderColor: 'rgba(255,99,132,1)',
						pointBackgroundColor: 'rgba(255,99,132,1)',
						pointBorderColor: '#fff',
						pointHoverBackgroundColor: '#fff',
						pointHoverBorderColor: 'rgba(255,99,132,1)',
						data: [28, 48, 40, 19, 96, 27, 100]
					}
				]
			}
		}
	}
}
</script>

<style scoped>

</style>
