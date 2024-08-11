<template>
	<main class="container" ref="containerRef">
		<Header />
		<Hero />
		<About />
		<History />
		<section class="fake-section"></section>
	</main>
</template>

<script setup>
import Header from '@/components/Header.vue';
import About from '@/components/About.vue';
import Hero from '@/components/Hero.vue';
import { onMounted, ref } from 'vue';
import History from '@/components/History.vue';

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
			threshold: 0.3
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
