<template>
	<div id="app" class="m">
	</div>
</template>

<script>
import { mapGetters } from 'vuex';
import { getCountriesAll } from '_store_/actions.js';
export default {
	name: 'app',
	components: {
	},
	data() {
		return {
			count: 1
		}
	},
	mounted() {
	},
	computed: {
		...mapGetters([''])
	},
	methods: {
	}
};
</script>
<style lang='scss' type='text/css'>
@import '~_scss_/app';
#app {
	background-color: $LightModeBackground;
}
</style>
<style type='text/css'>
@import '~_icomoon_/style.css';
</style>
