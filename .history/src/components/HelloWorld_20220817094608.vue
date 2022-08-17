
<template>
  <div class="search-wrapper panel-heading col-sm-12">
  <div id="overlay-id" class="overlay-content">
    <input type="text" v-model="search" placeholder="Search" /> 
    </div>
<div id="myOverlay" class="overlay">
  <span class="closebtn" onclick="closeSearch()" title="Close Overlay">x</span>
  <div class="overlay-content">
    <form action="action_page.php">
      <input type="text" placeholder="Search.." name="search">
      <button type="submit"><i class="fa fa-search"></i></button>
    </form>
  </div>
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

<style scoped>
.overlay {
    height: 100%;
    width: 100%;
    display: none;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
    background-color: rgb(0,0,0);
    background-color: rgba(0,0,0, 0.9); /* Black with a little bit see-through */
  }
  
  /* The content */
  #overlay-id {
    position: relative;
    top: 46%;
    width: 80%;
    text-align: center;
    margin-top: 30px;
    margin: auto;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    
  }
</style>