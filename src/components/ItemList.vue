<template>
  <div>
    <h3 class="title text-center text-uppercase font-weight-bold">All Books</h3>
    <p class="text-center">Total {{items.length}} Books in Store</p>
    <div class="row">
      <div class="col-md-2" v-for="item in items" :key="item.id">
          <div class="card">
            <img v-bind:src="item.cover" alt="Book cover image" class="card-img-top">
            <i class="fa fa-plus btn-success" @click="itemClicked(item)"></i>
            <div class="card-body">
              <h4 class="card-title">{{ item.title  }}</h4>
              <div class="card-text">{{ item.price | toTHB }}</div>
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
    }
  }
};
</script>


<style scoped>

.card {
    background-color: #fff;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
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
  /* text-overflow: ellipsis;
  overflow: hidden; 
  min-width: 160px; 
  height: 1.2em; 
  white-space: nowrap; */
}

.btn-success {
  font-size: 14px;
  background-color: #00B900;
  border-color: #00B900;
}

.card-img-top {
  height: 243px;
}
</style>