<template>
	<div>
		<div class="container" v-for="movie in movies" :key="movie.id">
			{{ movie.name }}
		</div>
		<loader
			:is-loading="loading"
			@intersect="load"
			@loading="onLoad"
		/>
	</div>
</template>
<script>
import Loader from '../components/Loader.vue'

export default {
	/**
	 * The component's registered child components.
	 *
	 * @type {Object}
	 */
	components: {
		Loader,
	},

	/**
	 * The component's computed properties.
	 *
	 * @type {Object}
	 */
	computed: {
		/**
		 * Get all the movies.
		 *
		 * @return {Array}
		 */
		movies() {
			return this.items
		},
	},


	/**
	 * The component's local methods.
	 *
	 * @type {Object}
	 */
	methods: {
		/**
		 * Load more movies.
		 *
		 * @return {void}
		 */
		load() {
			const size = this.items.length

			if(!this.loading) {
				return
			}
			for(let i = size; i <= size + 5; i++) {
				this.items.push({id: i+1, name: `Fast and Furious ${i+1}`})
			}
		},

		/**
		 * Handle the onLoad event.
		 *
		 * @return {void}
		 */
		onLoad(){
			this.loading = !this.loading

			if(this.loading) {
				this.load()
			}
		}
	},


	/**
	 * The component's name used for debugging.
	 *
	 * @type {String}
	 */
	name: 'Index',

	/**
	 * Get the component's initial state.
	 *
	 * @return {Object}
	 */
	data() {
		return {
			items: [ {id: 1, name: 'Fast and Furious 1'} ],
			loading: false,
		}
	},


}
</script>

<style>
	.container {
		align-content: flex-start;
		border: 1px solid black;
		display: flex;
		flex-wrap: wrap;
		height: 10rem;
		max-height: 65vh;
		overflow-x: hidden;
		padding: 1rem;
		position: relative;
	}
</style>
