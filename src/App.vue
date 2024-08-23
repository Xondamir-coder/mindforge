<template>
	<main class="container" ref="containerRef">
		<ScrollThingy />
		<Header />
		<Hero />
		<About />
		<History />
		<Directions />
		<Courses />
		<Services />
		<Product />
		<Skills />
		<Words />
		<Offer />
		<Contacts />
		<Footer />
	</main>
</template>

<script setup>
import { onMounted, ref } from 'vue';
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

const containerRef = ref(null);

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
});
</script>

<style lang="scss" scoped>
.container {
	overflow: hidden;
}
</style>
