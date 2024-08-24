<template>
	<section class="offer section-padding">
		<div class="offer__lines"></div>
		<img ref="objRef" class="offer__obj" src="@/assets/images/offer-obj.png" alt="offer obj" />
		<div class="offer__left">
			<div class="offer__top">
				<div class="offer__icon-container">
					<IconChat class="offer__icon" />
				</div>
				<span>{{ $t('offer-label') }}</span>
			</div>
			<h1 class="offer__title">{{ $t('offer-title') }}</h1>
			<p class="offer__text">
				{{ $t('offer-text') }}
			</p>
			<div class="offer__content">
				<h2 class="offer__content-data">99%</h2>
				<div class="offer__content-divider"></div>
				<div class="offer__content-text">{{ $t('offer-client') }}</div>
			</div>
		</div>
		<div class="offer__right">
			<Cards :contents="contents" />
		</div>
	</section>
</template>

<script setup>
import { computed, onMounted, ref } from 'vue';
import IconChat from './icons/IconChat.vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);
import offerImg1 from '@/assets/images/offer-1.webp';
import offerImg2 from '@/assets/images/offer-2.webp';
import offerImg3 from '@/assets/images/offer-3.webp';
import offerImg4 from '@/assets/images/offer-4.webp';
import offerImg5 from '@/assets/images/offer-5.webp';
import Cards from '@/components/Cards.vue';
import { i18n } from '@/locales';

const objRef = ref();
const contents = computed(() => [
	{
		img: offerImg1,
		text: i18n.global.t('offer-text-1'),
		for: i18n.global.t('offer-for-1')
	},
	{
		img: offerImg2,
		text: i18n.global.t('offer-text-2'),
		for: i18n.global.t('offer-for-2')
	},
	{
		img: offerImg3,
		text: i18n.global.t('offer-text-3'),
		for: i18n.global.t('offer-for-3')
	},
	{
		img: offerImg4,
		text: i18n.global.t('offer-text-4'),
		for: i18n.global.t('offer-for-4')
	},
	{
		img: offerImg5,
		text: i18n.global.t('offer-text-5'),
		for: i18n.global.t('offer-for-5')
	}
]);

onMounted(() => {
	gsap.to(objRef.value, {
		y: 200,
		scrollTrigger: {
			trigger: '.offer',
			scrub: 1,
			start: '-=50'
		}
	});

	// setInterval(() => {
	// 	changeCurSlide('next');
	// }, 8000);
});
</script>

<style lang="scss" scoped>
.offer {
	color: #fff;
	background-image: linear-gradient(to right bottom, #154c79, #0f3757, #0d2c43, #0b1e31, #091227);
	position: relative;
	overflow: hidden;
	padding-top: 15rem;
	padding-bottom: 15rem;
	display: grid;
	grid-template-columns: 40% minmax(0, 1fr);
	gap: 7rem;
	@media only screen and (max-width: 900px) {
		grid-template-columns: 100%;
		grid-auto-rows: max-content 1fr;
	}

	&.active &__left > *:not(.offer__text) {
		opacity: 1;
		transform: rotateY(0) translate(0, 0);
	}
	&.active &__text {
		opacity: 0.4;
		transform: rotateY(0) translate(0, 0);
	}

	&__left {
		position: relative;
		font-family: var(--font-alt);
		display: flex;
		flex-direction: column;
		gap: 4rem;
		& > * {
			// opacity: 0;
			// transform: rotateY(-100deg) translate(9rem, 9rem);
			transition: opacity 800ms, transform 800ms;
		}
	}
	&__right {
		position: relative;
	}
	&__content {
		display: flex;
		gap: 4rem;
		transition-delay: 600ms;
		&-divider {
			width: 1px;
			background-color: rgba(255, 255, 255, 0.2);
		}
		&-data {
			font-size: 5.5rem;
			font-weight: 600;
		}
		&-text {
			align-self: center;
			line-height: 26px;
		}
	}

	&__text {
		font-size: 17px;
		max-width: 80%;
		font-family: var(--font-base);
		line-height: 1.8;
		transition-delay: 400ms;
	}
	&__title {
		font-size: 5.5rem;
		line-height: 0.85;
		font-family: var(--font-alt);
		letter-spacing: -3px;
		font-weight: 600;
		transition-delay: 200ms;
	}
	&__obj {
		position: absolute;
		left: -10rem;
		top: 2rem;
	}
	&__lines {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-image: url('@/assets/images/hero-lines.svg');
		background-size: 13.5rem;
	}
	&__top {
		display: flex;
		align-items: center;
		gap: 10px;
		font-size: 1.9rem;
		font-weight: 500;
	}
	&__icon {
		width: 2.2rem;
		height: 2.2rem;
		color: var(--dark-gray);
		&-container {
			display: grid;
			place-items: center;
			background-color: var(--base-color);
			border-radius: 50%;
			width: 5.5rem;
			height: 5.5rem;
		}
	}
}
</style>
