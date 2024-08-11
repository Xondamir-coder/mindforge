<template>
	<div class="scroll" ref="scrollRef" @click="scrollToTop">
		<p class="scroll__text">scroll</p>
		<div class="scroll__outer">
			<div class="scroll__inner"></div>
		</div>
	</div>
</template>

<script setup>
import lenis from '@/js/lenis';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { onMounted, ref } from 'vue';
gsap.registerPlugin(ScrollTrigger);

const scrollRef = ref();

const scrollToTop = () => {
	lenis.scrollTo(0, {
		duration: 2
	});
};

onMounted(() => {
	gsap.to(scrollRef.value.querySelector('.scroll__inner'), {
		height: '100%',
		scrollTrigger: {
			trigger: document.body,
			start: '+=400',
			end: 'bottom bottom',
			scrub: 1
		}
	});
	gsap.from(scrollRef.value, {
		opacity: 0,
		scrollTrigger: {
			trigger: document.body,
			start: '+=400',
			toggleActions: 'play none none reverse'
		}
	});
});
</script>

<style lang="scss" scoped>
.scroll {
	position: fixed;
	z-index: 100;
	right: 3rem;
	top: 50%;
	transform: translateY(-50%);
	display: flex;
	align-items: center;
	flex-direction: column;
	gap: 15px;
	cursor: pointer;
	padding: 2rem;
	@media only screen and (max-width: 1200px) {
		display: none;
	}
	&__text {
		transform: rotate(180deg);
		writing-mode: vertical-lr;
		color: #000;
		font-weight: 700;
		font-size: 11px;
		text-transform: uppercase;
	}
	&__outer {
		height: 60px;
		width: 2px;
		background-color: #d9d9d9;
	}
	&__inner {
		background-color: #000;
		height: 0;
		width: 100%;
	}
}
</style>
