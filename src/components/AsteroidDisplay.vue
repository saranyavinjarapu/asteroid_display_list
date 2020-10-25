<template>
	<div>
		<button v-on:click="getAsteroidData">Display Asteroid Data</button>
		<table id="asteroid_table">
			<tr>
				<th>Asteroid Name</th>
				<th>Asteroid Id</th>
				<th>NASA JPN URL</th>
			</tr>
			<tr v-for="asteroidData in asteroidDataList" :key="asteroidData.id">
				<td>{{ asteroidData.name }}</td>
				<td>{{ asteroidData.id }}</td>
				<td>{{ asteroidData.nasa_jpl_url }}</td>
			</tr>
		</table>
	</div>
</template>

<script>
export default {
	name: "AsteroidDisplay",
	data() {
		return {
			asteroidDataList: []
		};
	},
	methods: {
		async getAsteroidData() {
			try {
				const response = await fetch(
					"https://api.nasa.gov/neo/rest/v1/neo/browse?api_key=ydl7nVUxNWm2Vid24ecGBL3L6R6dp8fHXbT4NfZO"
				);
				const json_data = await response.json();
				const near_earth_objects_data = json_data.near_earth_objects;
				const finalAsteroidData = [];
				for (var i = 0; i < 10; i++) {
					finalAsteroidData.push(near_earth_objects_data[i]);
				}
				this.asteroidDataList = finalAsteroidData;
			} catch (error) {
				console.log("error");
			}
		}
	}
};
</script>
<style scoped>
table {
	width: 80%;
	margin-left: auto;
	margin-right: auto;
	padding-top: 50px;
}
th,
td {
	border: 1px solid black;
	border-collapse: collapse;
	padding: 15px;
	text-align: left;
}

#asteroid_table tr:nth-child(even) {
	background-color: #eee;
}
#asteroid_table tr:nth-child(odd) {
	background-color: #fff;
}
#asteroid_table th {
	background-color: black;
	color: white;
}
button {
	padding: 10px;
	background-color: #1aa832;
	color: white;
	border: 1px solid #ccc;
	height: 50px;
	width: 400px;
	font-size: 30px;
	top: 3500px;
}
</style>
