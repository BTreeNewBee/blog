<style lang="stylus" rel="stylesheet/stylus">
@import './assets/stylus/article.styl'
@import './assets/stylus/hightlight.styl'

html, body, div
	margin 0
	padding 0
body
	font-size 14px
	font-family PingFang SC,Helvetica neue,Helvetica,Tahoma,lantinghei sc,Microsoft Yahei,sans-serif
	-webkit-font-smoothing antialiased
	background #21272c
a
	text-decoration none
#app
	font-family 'Avenir', Helvetica, Arial, sans-serif
	-webkit-font-smoothing antialiased
	-moz-osx-font-smoothing grayscale
	position relative
.view-outer
	min-height 100vh
	overflow hidden
.view-page
	position relative
	background #21272c
.view-animate-enter-active
	animation view-in 1.2s ease-in-out
.view-animate-leave-active
	animation view-out 1.2s ease-in-out
	transform-origin center bottom

@keyframes view-in
	0%,
	50%
		opacity 0
		transform translate(0, 200px)
	100%
		opacity 1
		transform translate(0, 0)
@keyframes view-out
	0%
		transform scale(1)
	50%,
	100%
		transform scale(0.88)
</style>
<template>
	<div id="app">
		<Navigation/>
		<div class="view-outer">
			<transition
				name="view-animate"
				@beforeLeave="beforeLeave"
				@afterLeave="afterLeave"
			>
				<router-view class="view-page" />
			</transition>
		</div>
	</div>
</template>

<script>
import './assets/stylus/animation.css'
import Navigation from './components/navigation/index.vue'
function getScrollTop () {
	return Math.max(document.documentElement.scrollTop, document.body.scrollTop)
}
export default {
	name: 'App',
	components: {Navigation},
	methods: {
		beforeLeave (node) {
			let scrollTop = getScrollTop()
			window.scrollTo(0, 0)
			node.style.position = 'absolute'
			node.style.top = '0px'
			node.style.left = '0px'
			node.style.zIndex = 0
			node.style.width = '100%'
			node.style.height = '100vh'
			node.style.overflow = 'hidden'
			node.scrollTop = scrollTop
		},
		afterLeave () {
			// window.scrollTo(0, 0)
		}
	}
}
</script>
