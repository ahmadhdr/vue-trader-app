<template>
  <div class="form-inline">
    <input 
      type="number" 
      class="form-control"
      v-model="quantity"
    >
    <button 
      class="btn btn-success"
      :disabled="quantity | notNegatif"
      @click.prevent="buyStock()"
    >
    Buy
    </button>
  </div>
</template>

<script>

import {
  Serializer
} from "../../../mixins"

export default {
  mixins: [Serializer],
  data(){
    return {
      quantity: 0
    }
  },
  props: ['stock'],
  methods: {
    buyStock() {
      const data = this.serialize(this.stock,this.quantity)
      this.eventHub.$emit('buy-stock',data)
      this.quantity = 0
    }
  },
  computed: {
 
  },
  filters: {
    notNegatif(value) {
      return value <= 0
    }
  }
}
</script>

<style>

</style>