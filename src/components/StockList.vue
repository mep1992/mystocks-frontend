<template>
    <div>
        <md-table md-card>
            <md-table-toolbar>
                <h1 class="md-title">Stock List</h1>
            </md-table-toolbar>

            <md-table-row>
                <md-table-head>Stock</md-table-head>
                <md-table-head md-numeric>Quantity</md-table-head>
            </md-table-row>

            <md-table-row v-for="(stock, quantity) in listData" :key="stock">
                <md-table-cell md-numeric>{{quantity}}</md-table-cell>
                <md-table-cell>{{stock}}</md-table-cell>
            </md-table-row>
        </md-table>
    </div>
</template>

<script>
  import axios from "axios";

  export default {
    name: "StockList",
    data: function () {
      return {
        listData: {},
      }
    },
    mounted() {
      this.getStockList();
    },
    methods: {
      getStockList() {
        const self = this
        const url = `${process.env.VUE_APP_BACKEND}api/stock/list`
        axios.get(url).then(function (response) {
          console.log('getStockList:', response.data)
          self.listData = response.data
        }).catch(function (error) {
          console.log(error)
        })
      }
    }
  }
</script>

<style scoped>
    .md-table {
        width: 50%;
        left: 25%;
        margin-top: 60px;
    }
</style>