

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
        <tr v-for="place in orders" :key="place.id">
            <td>{{place['order_name']}} </td>
            <td>{{place['id']}} </td>
            <td>{{ place['company_id']}} </td>
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
	async mounted(){
       var response = await fetch(`https://orders-go.herokuapp.com/orders`).then((response) => response.json())
  .then((data) => {
    this.orders   = [];
    // Getting every object from the array and pushing the names and images to OUR array
                data.forEach(item => {
                this.orders.push({ id: item.id, order_name: item.order_name, created_at: item.created_at, customer_id: item.customer_id });
        });
	
  });

		response = await fetch(`https://orders-go.herokuapp.com/order_items`).then((response) => response.json())
        .then((data) => {
    this.order_items   = [];
    // Getting every object from the array and pushing the names and images to OUR array
                data.forEach(item => {
                this.order_items.push({ id: item.id, order_id: item.order_id, price_per_unit: item.price_per_unit, quantity: item.quantity, product: item.product });
        });
	
  });
		

		response = await fetch(`https://orders-go.herokuapp.com/deliveries`).then((response) => response.json())
  .then((data) => {
    this.deliveries   = [];
    // Getting every object from the array and pushing the names and images to OUR array
                data.forEach(item => {
                this.deliveries.push({ id: item.id, order_item_id: item.order_item_id, delivered_quantity: item.delivered_quantity});
        });
	
		// console.log(this.deliveries[0].id)
  });

		response = await fetch(`https://orders-go.herokuapp.com/customers`).then((response) => response.json())
  .then((data) => {
     this.customer_names  = {};
	this.company_ids = {};
    // Getting every object from the array and pushing the names and images to OUR array
                data.forEach(item => {
					// this.customer_names.push({item.user_id: item.name,});
					this.customer_names[item.user_id.toString()] = item.name;
					this.company_ids[item.user_id.toString()] = item.company_id;
        });
	
		console.log(this.customer_names)
  });

		response = await fetch(`https://orders-go.herokuapp.com/customer_companies`).then((response) => response.json())
  .then((data) => {
    this.customer_companies   = [];
    // Getting every object from the array and pushing the names and images to OUR array
                data.forEach(item => {
					
                // this.customer_companies.push({ company_id: item.company_id, company_name: item.company_name});
        });
	
		// console.log(this.customer_companies[0].company_id)
  });
		
	
    },
	data() {
		
		return {
			input: {
				zipcode: ""
			},			
			orders: {},
			order_items: {},
			deliveries: {},
			customers: {},
			customer_companies: {},
			customer_names:{}
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
