<template>
	<div>
		<transition name="fade">
			<div class="login" v-show="loginIn">
				<div class="logo-wrapper">
					<logo :size="80"></logo>
				</div>
				<div class="register-wrapper">
					<div class="register">注&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;册</div>
					<div class="login-in" @click="mobileLogin">手机号登录</div>
				</div>
			</div>
		</transition>
	</div>
</template>

<script type="text/ecmascript-6">
	import logo from 'components/logo/logo';
	
	export default {
		components: {
			logo
		},
		data() {
			return {
				loginIn: true
			};
		},
		methods: {
			mobileLogin() {
				this.loginIn = false;
			}
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.login
		position: fixed
		left: 0
		top: 0
		width: 100%
		height: 100%
		z-index: 100
		background: url(loginbackground.jpg)
		background-size: 100% 100%
		background-repeat: no-repeat
		opacity: 1
		&.fade.enter-active, &.fade-leave-active
			transition: all 0.5s
		&.fade-enter, &.fade-leave-active
			opacity: 0
		.logo-wrapper
			position: absolute
			left: 50%
			top: 20%
			margin-left: -40px
		.register-wrapper
			position: absolute
			top: 60%
			width: 100%
			.register, .login-in
				margin: 30px auto 15px auto
				width: 80%
				height: 50px
				line-height: 50px
				text-align: center
				border-radius: 25px
				font-size: 18px
				font-weight: 700
				color: #fff
			.register
				background: #ff9900
			.login-in
				background: #990033
</style>