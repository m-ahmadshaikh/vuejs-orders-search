<<template v-for="block in content.body">
  <component :is="block.component" :block="block" :key="block._uid"></component>
</template>
<script>
import axios from 'axios'

export default {
	// eslint-disable-next-line vue/multi-word-component-names
	name: 'countrydetails',
	// Fetch the call for default Zip code
	async mounted(){
	// const result =	await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=1');
	// console.log("result is = " + result.data[0]);
    // console.log("result.title is = " + result.data.title);

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
