
<script>

import axios from 'axios';

//Version 1 - private function
function call(){
  return axios.get('https://jsonplaceholder.typicode.com/todos?_limit=1');
}

export default {
  name: 'app',
  components: {
    AddTodo
  },
  data(){
    return {
      todos: []
    }
  },

  methods: {
    // not allowed to use function keyword here  
    async printJson(){
      //make this.call(); if using version 2
      let result = await call();
      let data = result.data;
      console.log(data);
      for (let entry of data){
        console.log("result is = " + entry)
        console.log("result.title is = " + entry.title)
      }
    },   
    //Version 2 - public function
    call(){
      return axios.get('https://jsonplaceholder.typicode.com/todos?_limit=1');
    }
    ,addTodo(newTodo) {
      this.printJson()  
    }
  }
}
</script>