<template>
	<tr>
		<td width="120">
			<img src="http://via.placeholder.com/60x60" alt="">
		</td>

		<td>
			{{ product.product.name }} / {{ product.name }}
		</td>

		<td width="160">
			<div class="field">
				<div class="control">
					<div class="select is-fullwidth">
						<select v-model="quantity">
							<option value="0" v-if="product.quantity == 0">0</option>

							<option 
								:value="x"
								v-for="x in product.stock_count"
								:key="x"
								:selected="x == product.quantity"
							>{{ x }}</option>
						</select>
					</div>
				</div>
			</div>
		</td>

		<td>
			{{ product.total }}
		</td>

		<td>
			<button class="button is-text" @click="removeItem(product.id)">
				Remove
			</button>
		</td>
	</tr>
</template>

<script>
	import { mapActions } from 'vuex'

	export default {
		props: {
			product: {
				type: Object,
				required: true
			}
		},

		data () {
			return {
				quantity: this.product.quantity
			}
		},

		watch: {
			'quantity' (quantity) {
				this.updateItemQuantity({
					productId: this.product.id,
					quantity
				})
			}
		},

		methods: {
			...mapActions({
				removeItem: 'cart/destroy',
				updateItemQuantity: 'cart/update' 
			})
		}
	}
</script>