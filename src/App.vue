<template>
	<main class="container">
		<Header />
		<Hero />
		<section></section>
		<section></section>
	</main>
</template>

<script setup>
import Header from '@/components/Header.vue';
import Hero from './components/Hero.vue';
import Lenis from 'lenis';
const lenis = new Lenis();
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

function raf(time) {
	lenis.raf(time);
	requestAnimationFrame(raf);
}

requestAnimationFrame(raf);

lenis.on('scroll', ScrollTrigger.update);

gsap.ticker.add(time => {
	lenis.raf(time * 1000);
});

gsap.ticker.lagSmoothing(0);
</script>

<style lang="scss" scoped>
section {
	height: 100vh;
	background-color: yellow;
}
</style>
