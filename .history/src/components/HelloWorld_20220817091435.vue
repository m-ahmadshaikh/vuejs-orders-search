<template>
  <div id="app">
    <input v-model="searchQuery">
    <div v-for="r of resultQuery" :key="r.id">{{r.title}}</div>
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
      if (this.searchQuery) {
        return this.resources.filter(item => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every(v => item.title.toLowerCase().includes(v));
        });
      } else {
        return this.resources;
      }
    }
  }
};
</script>