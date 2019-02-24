<template>
  <div class="row">
    <div class="col-12 col-xs-2 col-sm-4 col-md-3 col-lg-3" v-for="item in items" :key="item.id">
      <div class="card mt-3">
        <img v-bind:src="item.cover" alt="Book cover image" class="card-img-top">
        <div class="card-body">
          <h4 class="card-title">{{ item.title }}</h4>
          <div class="row">
              <div class="col">
                  <p class="card-text">{{ formatPrice (item.price) | toTHB }}</p>
              </div>
              <div class="col">
                <button type="button" class="btn btn-primary btn-lg btn-block"  @click="itemClicked(item)">Add to Cart</button>
              </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ItemList',
  props: ["items", "add"],
  methods: {
    itemClicked(item) {
      this.add(item);
    },
    formatPrice(value) {
        let val = (value/1).toFixed(2).replace('.', '.')
        return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
    }
  }
};
</script>


<style scoped>

.card {
    border: none;
}

.card:hover {
    box-shadow: 0 0 11px rgba(33,33,33,.2); 
    -webkit-box-shadow: 0 0 11px rgba(33,33,33,.2); 
    -moz-box-shadow: 0 0 11px rgba(33,33,33,.2); 
    cursor: pointer;
}

.card-title {
    white-space:nowrap;
    overflow:hidden;
    text-overflow: ellipsis;
    display: block;
}


.card i {
    width: 50px;
    height: 50px;
    background: #ED277F;
    color: #ffffff;
    border-radius: 25px;
    text-align: center;
    line-height: 50px;
    font-size: 1.4rem;
    position: absolute;
    right: 6px;
    top: 209px;
    box-shadow: 0 0 4px 2px rgba(80, 80, 80, 0.1);
    cursor: pointer;
    transition: all 0.3s;
}
.card-text, .card-title {
  font-size: 14px;
}

.btn-success, .btn-block {
  font-size: 14px;
  background-color: #00B900;
  border-color: #00B900;
}

@media only screen and (min-width: 1200px) {
  .container {
    max-width: 960px !important;
  }
}

</style>