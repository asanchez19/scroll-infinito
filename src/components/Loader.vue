 <template>
	<div>
		<a href="#" @click.prevent="onLoaderClick">
			<span v-if="isLoading">Loading more...</span>
			<span v-else>Load more...</span>
		</a>
	</div>
</template>
<script>
export default {
	/**
	 * The component's local methods.
	 *
	 * @type {Object}
	 */
	methods: {
		/**
		 * Handle the loader click event.
		 *
		 * @return {void}
		 */
		onLoaderClick() {
			this.$emit('loading')
		},

		/**
		 * Determine if the intersect event should be emitted.
		 *
		 * @param {Object} entry
		 * @return {Boolean}
		 */
		shouldEmitIntersectEvent(entry) {
			if (!this.isLoading) {
				return false
			}

			return entry && entry.isIntersecting
		},
	},

	/**
	 * The component's name used for debugging.
	 *
	 * @type {String}
	 */
	name: 'Loader',

	/**
	 * The component's inherited properties.
	 *
	 * @type {Object}
	 */
	props: {
		/**
		 * Determine if the content loader is loading.
		 *
		 * @type {Array}
		 */
		isLoading: {
			type: Boolean,
			required: true,
		},

		/**
		 * The intersection observer API's options.
		 *
		 * @type {Object}
		 */
		options: {
			type: Object,
			default() {
				return {}
			},
		},
	},

	/**
	 * The component's mounted lifecycle hook.
	 *
	 * @return {void}
	 */
	mounted() {
		this.observer = new IntersectionObserver(([entry]) => {
			if (this.shouldEmitIntersectEvent(entry)) {
				this.$emit('intersect', entry)
			}
		}, this.options)

		this.observer.observe(this.$el)
	},

	/**
	 * The component's destroyed lifecycle hook.
	 *
	 * @return {void}
	 */
	destroyed() {
		this.observer.disconnect()
	},

	/**
	 * Get the component's initial state.
	 *
	 * @return {Object}
	 */
	data() {
		return {
			observer: null,
		}
	},
}
</script>
