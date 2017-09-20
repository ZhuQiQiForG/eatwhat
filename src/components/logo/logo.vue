<template>
	<div class="logo" :class="logoSize">
		<i class="icon-stumbleupon2"></i>
		<h1 class="title">去&nbsp;&nbsp;哪</h1>
	</div>
</template>

<script type="text/ecmascript-6">
	export default {
		props: {
			size: {
				type: Number
			}
		},
		computed: {
			logoSize () {
				return 'logo-' + this.size;
			}
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.logo
		font-size: 0
		color: #fff
		&.logo-80
			.icon-stumbleupon2
				font-size: 80px
			.title
				font-size: 30px
				font-weight: 700
				text-align: center
</style>