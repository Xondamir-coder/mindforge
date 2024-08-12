<template>
	<main class="container" ref="containerRef">
		<ScrollThingy />
		<Header />
		<Hero />
		<About />
		<History />
		<Services />
		<Product />
		<Skills />
		<Words />
		<Offer />
		<Contacts />
		<Cta />
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
import Cta from './components/Cta.vue';
import Contacts from './components/Contacts.vue';
import Footer from './components/Footer.vue';

const containerRef = ref();

onMounted(() => {
	const observer = new IntersectionObserver(
		entries => {
			entries.forEach(entry => {
				if (entry.isIntersecting) {
					entry.target.classList.add('active');
				} else {
					entry.target.classList.remove('active');
				}
			});
		},
		{
			threshold: 0.2
		}
	);

	containerRef.value.querySelectorAll('section').forEach(section => observer.observe(section));
});
</script>

<style lang="scss" scoped>
.fake-section {
	height: 100vh;
	background-color: purple;
}
</style>
