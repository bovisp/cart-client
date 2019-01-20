<template>
	<div class="section">
	  <div class="container is-fluid">
	    <div class="columns is-centered">
	      <div class="column is-three-quarters">
	        <h1 class="title is-4">Your cart</h1>

	        <article class="message" v-if="count">
	          <cart-overview />
	        </article>

	        <p v-else>
	        	Your cart is empty
	        </p>

	        <nuxt-link
	          :to="{ name: 'checkout' }"
	          class="button is-fullwidth is-info is-medium"
	          v-if="!empty"
	        >
	          Checkout
	        </nuxt-link>
	      </div>
	    </div>
	  </div>
	</div>
</template>

<script>
	import CartOverview from '../../components/cart/CartOverview'
	import { mapGetters } from 'vuex'

	export default {
		components: {
			CartOverview
		},

		computed: {
			...mapGetters({
				empty: 'cart/empty',
				count: 'cart/count'
			})
		}
	}
</script>