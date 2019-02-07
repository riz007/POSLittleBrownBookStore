<template>
    <div>
      <div class="row mb-3">
        <div class="col-md-9">
          <h1>Little Brown Book Shop</h1>
        </div>
        <div class="col-md-3">
           <Transaction :items="lineItems" :edit="toggleEdit" :remove="removeItem"></Transaction>
        </div>
      </div>

      <div class="row">
        <ItemList :items="items" :add="onItemClick"></ItemList>
      </div>
    </div>
</template>

<script>
import Transaction from "./Transaction";
import ItemList from "./ItemList";
import axios from "axios";

export default {
  components: {
    Transaction,
    ItemList
  },
  data() {
    return {
      items: [],
      lineItems: [],
      errors: []
    };
  },
  created () {
    axios.get(`https://api.jsonbin.io/b/5c52a1be15735a25423d3540`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.items = response.data.books;
    })
    .catch(e => {
      this.errors.push(e);
      // console.log('error');
    })
  },
  methods: {
    onItemClick: function(item) {
      // console.log("in", item);
      var found = false;
      for (var i = 0; i < this.lineItems.length; i++) {
        if (this.lineItems[i].item === item) {
          this.lineItems[i].numberOfItems++;
          found = true;
          break;
        }
      }
      if (!found) {
        this.lineItems.push({ item: item, numberOfItems: 1, editing: false });
      }
    },
    toggleEdit: function(lineItem) {
      lineItem.editing = !lineItem.editing;
    },
    removeItem: function(lineItem) {
      for (var i = 0; i < this.lineItems.length; i++) {
        if (this.lineItems[i] === lineItem) {
          this.lineItems.splice(i, 1);
          break;
        }
      }
    }
  }
};
</script>
<style>
</style>