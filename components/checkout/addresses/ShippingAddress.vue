<template>
	<article class="message">
      <div class="message-body">
        <h1 class="title is-5">Ship to</h1>

        <template v-if="selecting">
        	<shipping-address-selector 
				:addresses="addresses"
				:selectedAddress="selectedAddress"
				@click="addressSelected"
        	/>
        </template>

        <template v-else-if="creating">
        	<shipping-address-creator 
				@cancel="creating = false"
				@created="created"
        	/>
        </template>

		<template v-else>
	        <template v-if="selectedAddress">
	        	{{ selectedAddress.name }}<br>
	        	{{ selectedAddress.address_1 }}<br>
	        	{{ selectedAddress.city }}<br>
	        	{{ selectedAddress.postal_code }}<br>
	        	{{ selectedAddress.country.name }}<br>

	        	<br>
	        </template>

	        <div class="field is-grouped">
	        	<p class="control">
	        		<button 
	        			class="button is-info"
	        			@click="selecting = true"
	        		>
	        			Change shipping address
	        		</button>
	        	</p>

	        	<p class="control">
	        		<button 
	        			class="button is-info"
	        			@click="creating = true"
	        		>
	        			Add an address
	        		</button>
	        	</p>
	        </div>
        </template>        
      </div>
    </article>
</template>

<script>
	import ShippingAddressSelector from './ShippingAddressSelector'
	import ShippingAddressCreator from './ShippingAddressCreator'

	export default {
		components: {
			ShippingAddressSelector,
			ShippingAddressCreator
		},

		props: {
			addresses: {
				type: Array,
				required: true
			}
		},

		data () {
			return {
				localAddresses: this.addresses,
				selectedAddress: null,
				selecting: false,
				creating: false
			}
		},

		computed: {
			defaultAddress () {
				return this.localAddresses.find(address => address.default === true)
			}
		},

		methods: {
			addressSelected (address) {
				this.switchAddress(address)

				this.selecting = false
			},

			switchAddress (address) {
				this.selectedAddress = address
			},

			created (address) {
				this.localAddresses.push(address)

				this.creating = false

				this.switchAddress(address)
			}
		},

		created () {
			if (this.addresses.length) {
				this.switchAddress(this.defaultAddress)
			}
		}
	}
</script>