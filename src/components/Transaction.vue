<template>
    <div>
        <button id="cartBtn" class="btn btn-warning text-uppercase font-weight-bold" data-toggle="modal" data-target="#shoppingCart"><span class="fa fa-shopping-basket fa-fw" style="margin-right: 5px;"></span><span>Basket ({{ items.length }})</span></button>
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
                            <th></th>
                            <th>Book Title</th>
                            <th>Quantity</th>
                            <th>Amount</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in items" :key="item.id" class="border-bottom">
                        <td><img v-bind:src="item.item.cover" alt="Book cover image" class="circle-img"></td>
                        <td>{{ item.item.title }}</td>
                        <td>
                            <span v-if="!item.editing" @dblclick="toggleEdit(item)">{{ item.numberOfItems }}</span>
                            <input v-if="item.editing" @blur="toggleEdit(item)" type="number" v-model="item.numberOfItems">
                        </td>
                        <td>{{ item.numberOfItems * item.item.price }}</td>
                        <td class="text-center">
                            <button class="btn btn-sm btn-danger"  @click="removeItem(item)"><i class="fa fa-close"></i></button>
                        </td>
                        </tr>
                        <tr>
                            <td></td>
                            <th colspan="2">Subtotal:</th>
                            <td>{{ subtotal  }}</td>
                        </tr>
                        <tr>
                            <td></td>
                            <th colspan="2">Discount:</th>
                            <td>{{ discount }}</td>
                        </tr>
                        <tr>
                            <td></td>
                            <th colspan="2">Total:</th>
                            <td>{{ total | toTHB }}</td>
                        </tr>
                    </tbody>
                    </table>
                    <p v-if="!items.length">No items have been added.</p>
                </div>
                <div class="modal-footer">
                    <button class="btn btn-secondary" data-dismiss="modal">Go Back</button>
                    <button class="btn btn-line" @click='checkout'>Check out</button>
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

            var bookId = item.item.id;
            var bookTitle = item.item.title;
            let uniqueArray = [...new Set([bookId])];

            if(bookTitle.startsWith('Harry Potter') && uniqueArray && item.numberOfItems == 2) {
                discount = 0.1;
            } else if(bookTitle.startsWith('Harry Potter') && uniqueArray && item.numberOfItems == 3) {
                discount = 0.11;
            } else if(bookTitle.startsWith('Harry Potter') && uniqueArray && item.numberOfItems == 4) {
                discount = 0.12;
            } else if(bookTitle.startsWith('Harry Potter') && uniqueArray && item.numberOfItems == 5) {
                discount = 0.13;
            } else if(bookTitle.startsWith('Harry Potter') && uniqueArray && item.numberOfItems == 6) {
                discount = 0.14;
            } else if(bookTitle.startsWith('Harry Potter') && uniqueArray && item.numberOfItems == 6) {
                discount = 0.15;
            } else {
                discount = 0;
            }
        });

        return this.subtotal * discount;   
    },
    total: function() {
      return this.subtotal - this.discount;
    }
  },
  methods: {
    toggleEdit: function(item) {
      this.edit(item);
    },
    removeItem: function(item) {
      this.remove(item);
    },
    checkout() {
        alert('Pay us ฿' + this.total);
    }
  }
};
</script>

<style>
.modal-header {
    background-color: #00b900;
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
    background-color: #00b900;
    color: #ffffff;
}

#cartBtn {
    position: fixed;
    z-index: 999;
    top: 3%;
    right: 17%;
}

.circle-img {
    border-radius: 10%;
    -moz-border-radius: 10%;
    -webkit-border-radius: 10%;
    width: 50%;

}

.table td, .table th {
    border-top: none;
}

.border-bottom {
    border-bottom: 2px solid #dee2e6;
}
</style>