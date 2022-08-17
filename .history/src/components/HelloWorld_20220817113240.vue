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
	mounted(){
        axios.get(`https://api.zippopotam.us/in/600028`)
        .then(response => { 
            this.zipcode = response.data.origin;
            this.countrydetails = response.data;
        }).catch(error => { 
        })
  
    },,
	data() {
		return {
			input: {
				zipcode: ""
			},			
			countrydetails: {}
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
