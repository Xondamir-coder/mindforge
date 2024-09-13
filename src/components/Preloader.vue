<template>
	<div class="preloader">
		<div class="preloader__content">
			<div class="preloader__icons">
				<Icon class="preloader__icons-icon" />
				<div class="preloader__container">
					<IconText class="preloader__icons-text" />
				</div>
			</div>
			<p class="preloader__text">Loading {{ loadingNum }}%</p>
		</div>
	</div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import Icon from './Icon.vue';
import IconText from './IconText.vue';
import lenis from '@/js/lenis';
import gsap from 'gsap';

const loadingNum = ref(0);

const removeEl = () => {
	document.body.classList.remove('preloader-active');
	lenis.start();
	document.querySelector('.preloader').remove();
};
const startAnimation = () => {
	gsap.timeline()
		.to('.preloader__container', {
			width: 'auto',
			marginLeft: '3rem',
			duration: 0.7
		})
		.to('.preloader', {
			opacity: 0,
			duration: 1,
			onComplete: removeEl
		});
};

onMounted(() => {
	document.body.classList.add('preloader-active');
	lenis.stop();
	const interval = setInterval(() => {
		if (loadingNum.value < 100) {
			loadingNum.value++;
		} else {
			clearInterval(interval);
			startAnimation();
		}
	}, 20);
});
</script>

<style lang="scss" scoped>
.preloader {
	position: fixed;
	inset: 0;
	width: 100vw;
	height: 100vh;
	z-index: 200;
	display: grid;
	place-items: center;
	background-color: #fff;
	&__content {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 3rem;
		@media only screen and (max-width: 768px) {
			gap: 1.5rem;
		}
		@media only screen and (max-width: 400px) {
			gap: 0;
		}
	}
	&__text {
		font-size: 2rem;
		font-family: var(--font-alt);
		color: #3752ff;
		font-weight: 500;
	}
	&__container {
		width: 0;
		overflow: hidden;
	}
	&__icons {
		display: flex;
		align-items: center;
		&-icon {
			@media only screen and (max-width: 768px) {
				width: 16rem;
			}
			@media only screen and (max-width: 400px) {
				width: 10rem;
			}
		}
		&-text {
			@media only screen and (max-width: 768px) {
				width: 35rem;
			}
			@media only screen and (max-width: 400px) {
				width: 25rem;
			}
		}
	}
}
</style>
