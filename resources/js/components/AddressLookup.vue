<template>
  <div>
    <Postcode @postcode="loadAddresses($event)" />

    <ul v-show="addresses.length > 0 && show" class="list-group">
      <li v-for="address in addresses" class="list-group-item list-group-item-success" @click="select(address)">{{ address.line_1 }}</li>
    </ul>
  </div>
</template>

<script>
import Postcode from './Postcode'

export default {
  name: 'AddressLookup',
  data: function () {
    return {
      addresses: [],
      show: false
    }
  },
  methods: {
    loadAddresses (postcode) {
      fetch('https://addresses.iamproperty.com/postcodes/' + postcode + '/addresses')
      .then(r => r.json())
      .then(j => {
        this.show = true
        this.addresses = j.result
      })
    },
    select(v) {
      this.show = false
      this.$emit('select', v)
    }
  },
  components: {
    Postcode
  }
}
</script>

<style scoped>

</style>
