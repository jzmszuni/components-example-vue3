<template>
	<div class="card m-1 rounded-0 border-0">
		<div class="card-body bg-dark text-secondary">
			<h5 class="card-title">{{ id }} - Title: {{ title }}</h5>
			<p>{{ body }}</p>
			<button 
				@click="emit('cFavorite', title)"
				class="btn btn-sm btn-outline-success"
			>
				Favorito
			</button>
		</div>
	</div>
</template>

<script setup>
	// para hacer operaciones con los props hay que guardarlos en una const
	// const myProps = defineProps([
	// 	'id',
	// 	'title',
	// 	'body'
	// ])

	defineProps({
		id: Number,
		body: {
			type: String,
			default: "Sin infomración",
		},
		title: {
			type: String,
			default: "Sin título",
		}
	})

	const emit = defineEmits([
		'cFavorite'
	])
	
</script>

<style lang="sass" scoped>

</style>