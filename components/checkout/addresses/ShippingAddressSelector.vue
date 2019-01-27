<template>
	<table class="table is-hoverable is-fullwidth">
		<tbody>
			<tr
				v-for="address in addresses"
				:key="address.id"
			>
				<td>
					<p 
						:class="{ 'has-text-weight-bold': selectedAddress.id === address.id}"
					>
						{{ address.name }}<br>
			        	{{ address.address_1 }}<br>
			        	{{ address.city }}<br>
			        	{{ address.postal_code }}<br>
			        	{{ address.country.name }}<br>
		        	</p>
				</td>

				<td>
					<button class="button is-info" @click="$emit('click', address)">
						Ship here
					</button>
				</td>
			</tr>
		</tbody>
	</table>
</template>

<script>
	export default {
		props: {
			addresses: {
				type: Array,
				required: true
			},
			selectedAddress: {
				type: Object,
				required: true
			}
		}
	}
</script>