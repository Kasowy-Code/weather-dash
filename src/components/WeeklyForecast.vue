<script>
export default {
	props: {
		data: {
			type: Object,
			required: true
		}		
	},
}
</script>

<template>
	<!-- <div> -->
		<div id="weatherForecastContainer">
			<div class="weatherForecastTile"  v-for="element in this.data.list">
				<div class="weatherInfo">
					<h3>{{ new Date(element.dt*1000).toLocaleDateString('en-US', {weekday: "long"}) }}
						<span>{{ new Date(element.dt*1000).getDate() }}</span>
						<span>, {{ new Date(element.dt*1000).getHours().toString().padStart(2, '0') }}:{{ new Date(element.dt*1000).getUTCMinutes().toString().padStart(2, '0') }}</span>
					</h3>
					<img :src="'https://openweathermap.org/img/wn/'+element.weather[0].icon+'@2x.png'" alt="icon">
					<h2><span class="accent"> {{ (element.main.temp-273.15).toFixed(1) }} </span> °C</h2>
					<h3>{{ element.weather[0].description }}</h3>
					<h4>{{ element.main.pressure }} hPa</h4>
					<h4>{{ element.main.humidity }} % humidity</h4>
				</div>
			</div>
		</div>
	<!-- </div> -->
</template>
