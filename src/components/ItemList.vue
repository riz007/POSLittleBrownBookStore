<template>
  <div>
    <h3 class="title text-center">All Books</h3>
    <p class="text-center">Total {{items.length}} books</p>
    <div class="row">
      <div class="col-md-2" v-for="item in items" :key="item.id">
          <div class="card item-hover" @click="itemClicked(item)">
            <img v-bind:src="item.cover" alt="Book cover image" class="card-img-top">
            <div class="card-body">
              <h4 class="card-title">{{ item.title  }}</h4>
              <div class="card-text">{{ item.price | toTHB }}</div>
              <div class="row justify-content-center">
                <button class="btn btn-success" @click="itemClicked(item)">Add to cart</button>
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
    }
  }
};
</script>


<style scoped>
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

.item-hover {
  cursor: pointer;
}

.card-img-top {
  height: 243px;
}
</style>