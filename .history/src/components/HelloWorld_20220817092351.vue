<template>
  <div id="app">
  <div class="search-wrapper panel-heading col-sm-12">
    <input type="text" v-model="search" placeholder="Search" /> 
    

    
  </div>  
  <table class="table" id="myTable">
    <thead>
      <tr>
          <th>ID</th>
          <th>Name</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="product in filteredProducts" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.name }}</td>
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
      products: [
        {id: 1, name: "Foo"},
        {id: 2, name: "Bar"},
        {id: 3, name: "Baz"},
        {id: 4, name: "Foobar"}
      ],
      search: ""
    };
  },
  computed: {
    filteredProducts() {
      return this.products.filter(p => {
        // return true if the product should be visible

        // in this example we just check if the search string
        // is a substring of the product name (case insensitive)
        return p.name.toLowerCase().indexOf(this.search.toLowerCase()) != -1;
      });
    }
  }
};
</script>