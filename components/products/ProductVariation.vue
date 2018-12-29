<template>
	<div class="field">
		<label :for="type" class="label">
			{{ type }}
		</label>

		<div class="control">
			<div class="select is-fullwidth">
				<select :id="type">
					<option value="">Please choose...</option>

					<option 
						v-for="variation in variations"
						:key="variation.id"
					>{{ variation.name }}</option>
				</select>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			type: {
				required: true,
				type: String
			},
			variations: {
				required: true,
				type: Array
			}
		}
	}
</script>