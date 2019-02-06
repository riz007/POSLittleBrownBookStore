<template>
  <div>
      <h1 class="title">All Books</h1>
      <p>Total {{items.length}} books</p>

      <div class="row">
        <div class="col-md-2" v-for="item in items" :key="item.id">
          <div class="card">
            <img class="card-img-top" v-bind:src="item.cover" alt="Book cover image">
            <div class="card-body">
              <p class="card-text">{{ item.title }}</p>
              <p class="card-text">{{ item.price | toTHB }}</p>
              <a href="#" class="btn btn-primary"  @click="itemClicked(item)">Add</a>
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


<style>
.card-text {
  font-size: 14px;
}
</style>