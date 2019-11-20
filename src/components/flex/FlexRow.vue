<template>
	<div id="flex-row" class="m-60" ref="row">
		content
	</div>
</template>

<script>
export default {
	name: 'app',
	components: {
	},
	data() {
		return {
			dragging: false,
			previousPosition: null,
			parentWidth: null,
			parentPaddingLeft: null,
			clickOffSet: null,
			dragSide: null
		}
	},
	methods: {
		resize(event) {
			if (this.dragging) {
				if (this.dragSide == 'left') {
					let val = (((this.parentWidth/2) + this.parentPaddingLeft) - (event.pageX + this.clickOffSet)) / (this.parentWidth/2);
					this.$refs['row'].style.width = `${val * 100}%`;
				}else {
					this.$refs['row'].style.width = `${((event.pageX - (this.$refs['row'].offsetLeft) - this.clickOffSet) / this.parentWidth) * 100}%`;
				}
			}
		}
	},
	mounted() {
		let row = document.querySelector('#flex-row');
		const that = this;
		row.onmousedown = function(event) {
			document.addEventListener('mousemove', that.resize);
			if (event.offsetX < 0) that.dragSide = 'left';
			if (event.offsetX > row.getBoundingClientRect().width) that.dragSide = 'right';
			if (that.dragSide) {
				that.dragging = true;
				let computedParent = window.getComputedStyle(this.parentElement, null);
				that.parentWidth = Number(computedParent.getPropertyValue("width").replace('px', '')) - Number(computedParent.getPropertyValue('padding-left').replace('px', '')) * 2;
				that.parentPaddingLeft = Number(computedParent.getPropertyValue('padding-left').replace('px', ''));
				if (that.dragSide == 'right') that.clickOffSet = event.clientX - (row.offsetLeft + row.clientWidth);
				if (that.dragSide == 'left') that.clickOffSet = row.offsetLeft - event.clientX 
			}
		}
		document.addEventListener('mouseup', () => {
			this.dragging = false;
			document.removeEventListener('mousemove', this.resize);
		});
	},
	computed: {
	}
};
</script>
<style lang='scss' type='text/css'>
#flex-row {
	position: relative;
	margin-left: auto;
	margin-right: auto;
	width: 50%;
	user-select: none;
	&::before {
		content: '';
		position: absolute;
		transform-origin: right;
		background-color: gray;
		width: 20px;
		height: 100%;
		right: 100%;
	}
	&::after {
		content: '';
		position: absolute;
		transform-origin: right;
		background-color: gray;
		width: 20px;
		height: 100%;
		left: 100%;
	}
}
</style>
