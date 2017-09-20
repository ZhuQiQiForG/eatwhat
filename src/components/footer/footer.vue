<template>
	<div class="footer">
		<div class="location">
			<i class="icon-location2"></i>
		</div>
		<div class="userCenter">
			<i class="icon-menu"></i>
		</div>
	</div>
</template>

<script type="text/ecmascript-6">
	export default {};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.footer
		position: fixed
		display: flex
		left: 0
		bottom: 0
		height: 50px
		line-height: 50px
		width: 100%
		.location, .userCenter
			flex: 1
			display: inline-block
		.location
			text-align: left
		.userCenter
			text-align: right
</style>