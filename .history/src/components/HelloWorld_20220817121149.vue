

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
				<div align = "center">
      <table v-bind:transactinfo = "transactinfo">
        <tr>
            <th>Order Name</th>
            <th>Customer Company</th>
            <th>Customer Name</th>
            <th>Order Date</th>
            <th>Delivered amount</th>
            <th>Total amount</th>
        </tr>
        <tr v-for="place in countrydetails" :key="place.id">
            <td>{{place['order_name']}} </td>
            <td>{{place['id']}} </td>
            <td>{{place['id']}} </td>
            <td>{{place['created_at']}} </td>
            <td>12$ </td>
            <td>10$ </td>
        </tr>
     </table>
    </div>
			</div>
		</div>
	</div>
</template>

<script>
import axios from 'axios'

class OrderModel {
  constructor(id, created_at, ordername, customer_id) {
    this.id = id;
	this.created_at = created_at;
	this.ordername = ordername;
	this.customer_id = customer_id;
  }

}
export default {
	// eslint-disable-next-line vue/multi-word-component-names
	name: 'countrydetails',
	// Fetch the call for default Zip code
	mounted(){
        axios.get(`https://orders-go.herokuapp.com/orders`)
        .then(response => { 
            this.zipcode = response.data.origin;
            this.countrydetails = response.data;
        }).catch(error => { 
        })
		
  
    },
	data() {
		//create List of UserModel


var arr = this.companydetails.

		// this.user = new UserModel(response.data)
		for (var i = 0; i < arr.length; i++){
  document.write("<br><br>array index: " + i);
  var obj = arr[i];
  for (var key in obj){
    var value = obj[key];
    document.write("<br> - " + key + ": " + value);
  }
}
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
td {
  text-align: center;
  vertical-align: middle;
}
.addmargin {
	margin-top: 10px;
	margin-bottom: 10px;
}

.vue-logo-back {
	background-color: black;
}
</style>
