<template>
  <div id="app">
  <div class="search-wrapper panel-heading col-sm-12">
    <input type="text" v-model="search" placeholder="Search" /> <br> <br>
  </div>  
  <table class="table" id="myTable">
      <thead>
      <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Category</th>
          <th>Quantity</th>
          <th>Status</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="product in searchProd" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.category }}</td>
          <td>{{ product.quantity }}</td>
          <td>{{ product.status }}</td>
      </tr>
      </tbody>
  </table>
</div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      searchQuery: null,
      resources: [
        {id: 1, name:'Prod 1', category: 'Cat 1', quantity: 3, status: true},
          {id: 2, name:'Prod 2', category: 'Cat 2', quantity: 5, status: true},
          {id: 3, name:'Prod 3', category: 'Cat 1', quantity: 1, status: false},
          {id: 4, name:'Prod 4', category: 'Cat 3', quantity: 8, status: true},
          {id: 5, name:'Prod 5', category: 'Cat 1', quantity: 0, status: true}
      ]
    };
  },
  computed: {
    resultQuery() {
      let se = []
     if(this.search !== '') {
      se = this.resources.filter(p => 
        p.name.toLowerCase().includes(this.search.toLowerCase()) ||
        p.category.toLowerCase().includes(this.search.toLowerCase()) ||
        p.quantity === Number(this.search)
      )
     } else {
      se = this.resources
     }
     return se
      }
    }
  };
</script>