<template>
    <div>
        <table class="table table-striped table-hover table-bordered" v-if="items.length">
            <thead>
                <tr>
                    <th>Book Title</th>
                    <th>Quantity</th>
                    <th>Amount</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in items" :key="item.id">
                    <td>{{ item.item.title }}</td>
                    <td>
                        <span v-if="!item.editing" @dblclick="toggleEdit(item)">{{ item.numberOfItems }}</span>
                        <input v-if="item.editing" @blur="toggleEdit(item)" type="number" v-model="item.numberOfItems">
                    </td>
                    <td>{{ item.numberOfItems * item.item.price }}</td>
                    <td><a href="#" class="fa fa-times" @click="removeItem(item)"></a></td>
                </tr>
            </tbody>
        </table>
        <p v-if="!items.length">No items have been added.</p>

        <table class="table">
            <tbody>
                <tr>
                    <td>Subtotal:</td>
                    <td>{{ subtotal }}</td>
                </tr>
                <tr>
                    <td>Discount:</td>
                    <td>{{ discount }}</td>
                </tr>
                <tr>
                    <td>Total:</td>
                    <td>{{ total }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
  name: "Transaction",
  props: ["items", "edit", "remove"],
  computed: {
    subtotal: function() {
      var subtotal = 0;
      this.items.forEach(function(item) {
        subtotal += item.item.price * item.numberOfItems;
      });
      return subtotal;
    },
    discount: function() {
        var discount = 0;
        //  this.items.forEach(function(item) {
        //     if(item.numberOfItems == 2) {
        //         discount = 0.1;
        //         return subtotal - discount;
        //     }
        //     else if(item.numberOfItems == 3) {
        //         discount = 0.11;
        //         return this.subtotal - discount;
        //     }
        //     else if(item.numberOfItems == 4) {
        //         discount = 0.12;
        //         return this.subtotal - discount;
        //     }
        //     else if(item.numberOfItems == 5) {
        //         discount = 0.13;
        //         return this.subtotal - discount;
        //     }
        //     else if(item.numberOfItems == 6) {
        //         discount = 0.14;
        //         return this.subtotal - discount;
        //     }
        //     else if(item.numberOfItems == 7) {
        //         discount = 0.15;
        //         return this.subtotal - discount;
        //     }
        
        // });
        return this.subtotal * discount;
       
    },
    total: function() {
      return this.subtotal + this.discount;
    }
  },
  methods: {
    toggleEdit: function(item) {
      this.edit(item);
    },
    removeItem: function(item) {
      this.remove(item);
    }
  }
};
</script>