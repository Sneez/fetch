<template>
  <div class="table-wrapper">
      <h3>Fetch Rewards Exercise</h3>
      <b-table striped hover :items="itemList" :fields="fields"></b-table>
  </div>
</template>

<script>
export default {
  name: 'Fetch',
  data: function(){
    return{
      itemList: [],
      fields: ['listId', 'id', 'name']
    }
  },

  mounted() {
    this.getList();
  },

  methods: {

    async getList(){
      try {
        const res = await fetch("https://fetch-hiring.s3.amazonaws.com/hiring.json");
        const data = await res.json();
        this.itemList = this.filterAndSort(data);
        console.log(this.itemList);
      }
      catch {
        console.log('Error fetching results');
      }
    },

    filterAndSort(list){
      // filter out all data with falsy names, then sort
      return list.filter(data => data.name).sort(function(a, b){

        // if list id's are different, sort by list id
        if (a.listId < b.listId) {
          return -1;
        }
        if (a.listId > b.listId) {
          return 1;
        }

        // if list id's are the same, sort by id
        // since every name is simply 'Item {id}', sorting by id is cleaner and prevents
        // 'Item 3' from coming before 'Item 296'
        if (a.id < b.id) {
          return -1;
        }
        if (a.id > b.id) {
          return 1;
        }

        // do nothing if list id and name are the same
        return 0;
      });
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.table-wrapper{
  max-width: 1000px;
  margin: auto;
}

</style>
