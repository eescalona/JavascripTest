<template>
  <div id="app" class="container">
        <p>{{ tableTitle }}</p>
        <table class="table table-bordered">
            <thead class="thead-light">
                <th scope="col">#</th>
                <th scope="col">Name</th>
                <th scope="col">Account</th>
                <th scope="col">Value</th>
                <th scope="col">Created</th>
            </thead>
            <tr v-for="item in sortedFiltedList()" v-bind:class="getRowClass(item)">
                <th scope="row"> {{ item.id }} </th>
                <td> {{ item.name }} </td>
                <td> {{ item.account }} </td>
                <td> {{ item.value | twoDecimal }} </td>
                <td> {{ item.created | customDate}} </td>
            </tr>
        </table>
    </div>
</template>

<script>
  import moment from 'moment'
  export default {
    name: 'app',
    data() {
      return {
        tableTitle: 'Please see table bellow:',
        list: [
          {id: 1, name: 'Bob', account: 'ACC123', value: 500, created: "2017-01-11"},
          {id: 2, name: 'Alice', account: 'BBB321', value: 300, created: "2017-03-05"},
          {id: 3, name: 'Jim', account: 'BAA456', value: 20.5, created: "2017-02-12"},
          {id: 4, name: 'Liz', account: 'BBBB654', value: 1000, created: "2017-04-30"}
        ]
      }
    },
    methods: {
      sortedFiltedList: function() {
        let filterList = this.list.filter( (item) => {
          if ( item.account.startsWith('B'))
          {
            return item;
          }
        });
        return filterList.sort(function(a, b){
          if(a.account < b.account) return -1;
          if(a.account > b.account) return 1;
          return 0;
        });
      },
      getRowClass: function (item) {
        if (item.value < 100) {
          return 'table-danger';
        } else if (item.value > 500){
          return 'table-success';
        }
      }
    },
    filters: {
      customDate: function (date) {
        return new moment(date).format('D MMMM Y');
      },
      twoDecimal: function (num) {
        return parseFloat(num).toFixed(2);
      }
    }
  }
</script>

<style>
</style>
