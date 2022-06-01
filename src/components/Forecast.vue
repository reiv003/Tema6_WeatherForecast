<template>
	<div class="content">
		<div> {{ city }} </div>
		<br>
		<div> {{ tempToday }} </div>
		<div> {{ windToday }} </div>
		<div> {{ descToday }} </div>
		<br>
		<div> {{ forecastTemp1 }} </div>
		<div> {{ forecastWind1 }} </div>
		<br>
		<div> {{ forecastTemp2 }} </div>
		<div> {{ forecastWind2 }} </div>
		<br>
		<div> {{ forecastTemp3 }} </div>
		<div> {{ forecastWind3 }} </div>
		<button @click="changeCity">Endre by </button>
	</div>	
</template>

<script>
	export default {
		
		data() {
			return {
				city: 'bergen',
				forecastTemp1: '',
				forecastWind1: '',
				forecastTemp2: '',
				forecastWind2: '',
				forecastTemp3: '',
				forecastWind3: '',
				forecast: [],
				tempToday: '',
				windToday: '',
				descToday: ''

			}
		},

		created() {
			this.fetchNew();
		},

		methods: {
			async fetchNew() {
				/* This API sometimes does not return any data for a given city. If the site does not display any data, try changing the city field under data() return, or look directly at the API to see if the data is present there for that city. */

				let url = (`https://goweather.herokuapp.com/weather/${this.city}`);
				const res = await fetch(url);
				const { temperature, wind, description, forecast } = await res.json();
				console.log(res);
				console.log(temperature);
				console.log(wind);
				console.log(forecast);
				console.log(description);
				this.forecastTemp1 = forecast[0].temperature;
				this.forecastWind1 = forecast[0].wind;
				this.forecastTemp2 = forecast[1].temperature;
				this.forecastWind2 = forecast[1].wind;
				this.forecastTemp3 = forecast[2].temperature;
				this.forecastWind3 = forecast[2].wind;
				this.tempToday = temperature;
				this.descToday = description;
				this.windToday = wind;
				
		
			},
			/*Does not work yet*/
			changeCity() {
				this.city = 'bergen';
			}
		}
	}
</script>

<style>
	
</style>	