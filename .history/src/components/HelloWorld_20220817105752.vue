<template>
	<div class="home">
		<div class="vue-logo-back">
			<img src="../assets/logo.png"
				width="100px"
				height="100px" />
		</div>
		<div class="col-md-6 centeralign">
			<p>
				This Page Displays Country details
				by Zip Code. Example : 600 028
			</p>
			<input type="text"
				v-model="input.zipcode"
				placeholder="Zip Code" />
			<button v-on:click="getLocationDetails()">
				Get Location Details
			</button>
			<div class="card-body">
				<h5 class="card-title">
					{{countrydetails}}
				</h5>
				<p class="card-text">
					Zip Code : {{countrydetails["post code"]}}
				</p>

				<p class="card-text">
					Country : {{countrydetails.country}}
				</p>

				<p class="card-text">
					Country Short Form : {{countrydetails["country abbreviation"]}}
				</p>

				<ul>
					<li v-for="place in countrydetails.places" :key="place.longitude">
						<p class="card-text">
							Place Name : {{countrydetails}}
						</p>

						<p class="card-text">
							Longitude : {{place["longitude"]}}
						</p>

						<p class="card-text">
							Latitude : {{place["latitude"]}}
						</p>

						<p class="card-text">
							State : {{place["state"]}}
						</p>

						<p class="card-text">
							State Short Form : {{place["state abbreviation"]}}
						</p>
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
import axios from 'axios'

export default {
	// eslint-disable-next-line vue/multi-word-component-names
	name: 'countrydetails',
	// Fetch the call for default Zip code
	async mounted(){
	const result =	await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=1');
	console.log("result is = " + result.data[0]);
    console.log("result.title is = " + result.data.title);

	},
	data() {
		return {
			content: {
        body: [
          {
            _uid: "BUY6Drn9e1",
            component: "foo",
            headline: "Foo"
          },
          {
            _uid: "gJZoSLkfZV",
            component: "bar",
            title: "Bar"
          },
          {
            _uid: "X1JAfdsZxy",
            component: "foo",
            headline: "Another headline"
          }
        ]
      }
		}
	},

	methods: {
		// According to the given zipcode, the fetch is happening
		getLocationDetails() {
			axios.get(`https://api.zippopotam.us/in/`+this.input.zipcode)
			.then(function(response) {
				this.countrydetails = response.data;
			}.bind(this)).catch(error => {
			})			
		}
	}
}
</script>
<style scoped>
.addmargin {
	margin-top: 10px;
	margin-bottom: 10px;
}

.vue-logo-back {
	background-color: black;
}
</style>
