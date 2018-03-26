<template>
  <div>
    <div id="items_form">
      Add Items to your cart:
      <select v-model="item_name">
        <option v-for="item in item_names" v-bind:value="item">{{item}}</option>
      </select>
      <select v-model="item_count">
        <option v-for="n in item_counts" v-bind:value="n">{{n}}</option>
      </select>
      <button v-on:click="add_item"> Add</button>
    </div>

    <div id="item_listing">
      The Items you have added are: <br/>
      <ol>
          <li v-for="(item, key) in cart_items">
            {{item.name}} - {{item.number}} 
            <button v-on:click="remove_item(key)">remove</button>
          </li>
      </ol>
    </div>
  </div>
</template>

<script>
var fruits = ["apple", "banana", "orange", "spinatch", "lettuce"];
var defaults = [fruits[0], 1]
export default {
  name: 'ShoppingCart',
  data () {
    return {
      item_names: fruits,
      item_counts: [1,2,3,4,5],
      item_name: defaults[0],
      item_count: defaults[1],
      cart_items: [
        {name: "item1", number: 2},
        {name: "item2", number: 3}
      ]
    }
  },
  methods: {
    add_item: function(){
      this.cart_items.push({name: this.item_name, number: this.item_count});
      this.item_name = this.first_item;
      this.item_count = this.first_count;
    },
    remove_item: function(index){
      this.cart_items.splice(index, 1)
    }
  },
  computed:{
    first_item: function(){
      return this.item_names[0]
    },
    first_count: function(){
      return this.item_counts[0]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div#item_listing{
  margin-top: 10px;
  text-align: left;
  margin-left: 10px;
}

a {
  color: #42b983;
}
</style>
