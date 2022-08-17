

<template>
	<div class="home">
		

		<div >
			
			<input class="col-md-6 centeralign" type="text" style="width:400px;"
				v-model="searchQuery"  
				placeholder="Order Name" />
			
			<br>
			<br>
			<label for="startDate">Start Date</label>	
			<input v-model="start_date" type="date" name="startDate" placeholder="Start date" />
&nbsp;
			<label for="endDate">End Date</label>
            <!-- The end date field -->
            <input v-model="end_date" type="date" name="endDate" placeholder="End date" /><br><br>
			<div class="card-body">
				<div align = "center">
				
      <b-table class="col-md-6 centeralign" v-bind:orderinfo = "orderinfo">
        <tr>
            <th>Order Name</th>
            <th>Customer Company</th>
            <th>Customer Name</th>
            <th>Order Date</th>
            <th>Delivered amount</th>
            <th>Total amount</th>
        </tr>
        <tr v-for="place in resultQuery" :key="place.id">
            <td>{{place['order_name']}} </td>
            <td>{{customer_companies[company_ids[place['customer_id']]]}} </td>
            <td>{{ customer_names[place['customer_id']]}} </td>
            <td>{{place['created_at'] }} </td>
            <td>12$ </td>
            <td>10$ </td>
        </tr>
     </b-table>
    </div>
			</div>
		</div>
	</div>
</template>

<script>
import axios from 'axios'
import moment from "moment";
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
    // this.orders   = [];
    // Getting every object from the array and pushing the names and images to OUR array
                data.forEach(item => {

	var date  = moment(item.created_at).utc().format('LL, hh:mm a');
                this.orders.push({ id: item.id, order_name: item.order_name, created_at: date, customer_id: item.customer_id,check_date :moment(item.created_at) });
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
	
		// console.log(this.customer_names)
  });

		response = await fetch(`https://orders-go.herokuapp.com/customer_companies`).then((response) => response.json())
  .then((data) => {
    this.customer_companies   = {};
    // Getting every object from the array and pushing the names and images to OUR array
                data.forEach(item => {
					this.customer_companies[item.company_id.toString()] = item.company_name;
                // this.customer_companies.push({ company_id: item.company_id, company_name: item.company_name});
        });
	
		console.log(this.customer_companies)
  });
		
	
    },
	data() {
		
		return {
searchQuery: null,
start_date: moment("2000-11-07T09:00:13Z"),
  end_date: moment("2220-11-07T09:00:13Z"),
			
			orders: [],
			order_items: {},
			deliveries: {},
			customers: {},
			customer_companies: {},
			customer_names:{},
			company_ids:{}
      
		}
	},
   computed: {
    resultQuery(){
      if(this.searchQuery){
      return this.orders.filter((order) =>
    order.order_name.toString().toLowerCase().includes(this.searchQuery.toLowerCase() && order.check_date.isAfter(this.start_date)  && order.check_date.isBefore(this.end_date) )
  );
      }else{
        return this.orders.filter((order) => order.check_date.isAfter(this.start_date)  && order.check_date.isBefore(this.end_date)  );
      }
    }
  },

	methods: {
		// According to the given zipcode, the fetch is happening
		getLocationDetails() {
			


			var filteredData =  this.orders.filter((order) =>
    order.order_name.toString().toLowerCase().includes(this.input.text.toLowerCase())
  );
this.orders  = filteredData;

		} ,
		getFilteredByDate(){
			const filterDate = {
  start_date: "2019-11-07T09:00:13Z",
  end_date: "2019-11-07T09:00:13Z",
};

var filteredItems = this.orders.filter((item, index) => item.created_at >= this.input.start_date && item.created_at <= this.input.end_date);
		this.orders  = filteredItems;
    }
    
		
	}
}

</script>
import { ref } from "vue";
let input = ref("");
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
