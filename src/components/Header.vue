<template>
	<header class="header" ref="headerRef">
		<a href="#"><Logo class="header__logo" /></a>
		<a class="header__call" href="tel:+1 800 222 000">
			<IconCall class="header__call-icon" />
			<a>1 800 222 000</a>
		</a>
	</header>
</template>

<script setup>
import Logo from './icons/Logo.vue';
import IconCall from './icons/IconCall.vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { onMounted, ref } from 'vue';
gsap.registerPlugin(ScrollTrigger);
const headerRef = ref();

onMounted(() => {
	gsap.timeline({
		scrollTrigger: {
			trigger: headerRef.value,
			start: '+=200 top',
			endTrigger: document.body,
			toggleActions: 'play none none reverse'
		}
	})
		.to(headerRef.value, {
			y: '-100%'
		})
		.to(headerRef.value, {
			backgroundColor: '#fff',
			color: 'var(--dark-gray)',
			boxShadow: '0 0px 20px 4px rgba(0, 0, 0, 0.25)',
			y: 0,
			duration: 0.5
		});
});
</script>

<style lang="scss" scoped>
.header {
	width: 100%;
	display: flex;
	justify-content: space-between;
	position: fixed;
	z-index: 100;
	top: 0;
	padding: 2rem 4.5rem;
	font-family: var(--font-alt);
	// background-color: #fff;
	color: #fff;
	&__logo {
		width: 15.7rem;
		height: 3.9rem;
	}
	&__call {
		display: flex;
		align-items: center;
		gap: 1rem;
		font-size: 1.7rem;
		color: inherit;
		font-weight: bold;
		text-decoration: none;
		&-icon {
			width: 1.7rem;
			height: 1.7rem;
			fill: currentColor;
		}
	}
}
</style>
