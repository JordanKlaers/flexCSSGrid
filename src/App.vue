<template>
	<div id="app" class="m">
		<div class="container p-lft-30 p-rgt-30">
			<flex-row></flex-row>
		</div>
	</div>
</template>

<script>
import { mapGetters } from 'vuex';
import FlexRow from './components/flex/FlexRow';
export default {
	name: 'app',
	components: {
		'flex-row': FlexRow
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
	.container {
		display: flex;
	}
}
</style>
<style type='text/css'>
@import '~_icomoon_/style.css';
</style>
