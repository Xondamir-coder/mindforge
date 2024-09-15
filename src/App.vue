<template>
	<Preloader />
	<main class="container" ref="containerRef">
		<ScrollThingy />
		<Header />
		<Hero />
		<About />
		<History />
		<Directions />
		<Services />
		<!-- <Product />
		<Skills /> -->
		<Words />
		<Offer />
		<Courses />
		<Contacts />
		<Footer />
	</main>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue';
import Header from '@/components/Header.vue';
import About from '@/components/About.vue';
import Hero from '@/components/Hero.vue';
import History from '@/components/History.vue';
import ScrollThingy from '@/components/ScrollThingy.vue';
import Services from '@/components/Services.vue';
import Product from '@/components/Product.vue';
import Skills from './components/Skills.vue';
import Words from './components/Words.vue';
import Offer from './components/Offer.vue';
import Contacts from './components/Contacts.vue';
import Footer from './components/Footer.vue';
import Directions from './components/Directions.vue';
import Courses from './components/Courses.vue';
import Preloader from './components/Preloader.vue';

const containerRef = ref(null);

const func = () => window.scrollTo(0, 0);

onMounted(() => {
	const observer = new IntersectionObserver(
		entries => {
			entries.forEach(entry => {
				if (entry.isIntersecting) {
					entry.target.classList.add('active');
				}
			});
		},
		{
			threshold: window.innerWidth < 768 ? 0.1 : 0.2
		}
	);

	containerRef.value.querySelectorAll('section').forEach(section => observer.observe(section));

	window.addEventListener('unload', func);
});

onUnmounted(() => {
	window.removeEventListener('unload', func);
});
</script>

<style scoped>
.container > * {
	overflow: hidden;
}
</style>
