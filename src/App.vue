<template>
  <div id="app">
    <index/>
  </div>
</template>

<script>
import Index from './views/Index.vue'

export default {
	/**
	 * The component's registered child components.
	 *
	 * @type {Object}
	 */
	components: {
		Index,
	},

	/**
	 * The component's name used for debugging.
	 *
	 * @type {String}
	 */
	name: 'App',
}
</script>
