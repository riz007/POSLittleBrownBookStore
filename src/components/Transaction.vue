<template>
    <div>
        <button class="btn btn-warning text-uppercase font-weight-bold" data-toggle="modal" data-target="#shoppingCart"><span class="fa fa-shopping-basket fa-fw" style="margin-right: 5px;"></span><span>Basket ({{ items.length }})</span></button>
        <div id="shoppingCart" class="modal fade">
            <div class="modal-dialog modal-line">
                <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Customer's Basket</h5>
                    <button class="close" data-dismiss="modal">
                    &times;
                    </button>
                </div>
                <div class="modal-body">
                    <table class="table" v-if="items.length">
                    <thead>
                        <tr>
                            <th>Book Title</th>
                            <th>Quantity</th>
                            <th>Amount</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr  v-for="item in items" :key="item.id">
                        <td>{{ item.item.title }}</td>
                        <td>
                            <span v-if="!item.editing" @dblclick="toggleEdit(item)">{{ item.numberOfItems }}</span>
                            <input v-if="item.editing" @blur="toggleEdit(item)" type="number" v-model="item.numberOfItems">
                        </td>
                        <td>{{ item.numberOfItems * item.item.price }}</td>
                        <td>
                            <button class="btn btn-sm btn-danger"  @click="removeItem(item)"><i class="fa fa-close"></i></button>
                        </td>
                        </tr>

                        <tr>
                            <th colspan="2">Subtotal:</th>
                            <td>{{ subtotal }}</td>
                        </tr>
                        <tr>
                            <th colspan="2">Discount:</th>
                            <td>{{ discount }}</td>
                        </tr>
                        <tr>
                            <th colspan="2">Total:</th>
                            <td>{{ total }}</td>
                        </tr>
                        <th></th>
                    </tbody>
                    </table>
                    <p v-if="!items.length">No items have been added.</p>
                </div>
                <div class="modal-footer">
                    <button class="btn btn-secondary" data-dismiss="modal">Keep shopping</button>
                    <button class="btn btn-line">Check out</button>
                </div>
                </div>
            </div>
        </div>
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
    discount: function(item) {
        var discount = 0;

         this.items.forEach(function(item) {
            if(item.length == 2) {
                discount = 0.1;
                console.log(discount);
            }
            // else if(item.numberOfItems == 3) {
            //     discount = 0.11;
            //     return this.subtotal - discount;
            // }
            // else if(item.numberOfItems == 4) {
            //     discount = 0.12;
            //     return this.subtotal - discount;
            // }
            // else if(item.numberOfItems == 5) {
            //     discount = 0.13;
            //     return this.subtotal - discount;
            // }
            // else if(item.numberOfItems == 6) {
            //     discount = 0.14;
            //     return this.subtotal - discount;
            // }
            // else if(item.numberOfItems == 7) {
            //     discount = 0.15;
            //     return this.subtotal - discount;
            // }
        
        });
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

<style scoped>
.modal-header {
    background-color: #4ecd00;
    color: #ffffff;
}

.modal-header .close {
    color: #fff; 
    opacity: 1;
}

@media only screen and (min-width: 768px) {
    .modal-line {
        min-width: 768px;
        margin: auto;
    }
}

.modal-dialog {
    min-height: calc(100vh - 60px);
    display: flex;
    flex-direction: column;
    justify-content: center;
    overflow: auto;
}
@media(max-width: 768px) {
  .modal-dialog {
    min-height: calc(100vh - 20px);
  }
}

.btn-line {
    background-color: #4ecd00;
    color: #ffffff;
}
</style>