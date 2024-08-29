<template>
	<div class="container">
		<ScrollHere @click="scrollToAbout" />
		<section ref="aboutRef" class="about section-padding">
			<Rectangle class="about__rectangle" />
			<div class="about__top">
				<div class="about__left">
					<div class="about__left-head">
						<div class="about__icon-container">
							<IconAward class="about__icon" />
						</div>
						<span>{{ $t('about-label') }}</span>
					</div>
					<h1 class="about__title">{{ $t('about-title') }}</h1>
				</div>
				<div class="about__right">
					<h2 class="about__subtitle">
						{{ $t('about-subtitle') }}
					</h2>
					<p class="about__text">
						{{ $t('about-text') }}
					</p>
				</div>
			</div>
			<ul class="about__list">
				<li class="about__item" v-for="content in contents" :key="content">
					<div class="about__item-img">
						<img :src="content.img" alt="img" />
					</div>
					<h3 class="about__item-title">{{ content.title }}</h3>
					<p class="about__item-text">{{ content.text }}</p>
				</li>
			</ul>
		</section>
	</div>
</template>

<script setup>
import lenis from '@/js/lenis';
import { computed, onMounted, ref } from 'vue';
import IconAward from './icons/IconAward.vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import ScrollHere from './ScrollHere.vue';
import Rectangle from './Rectangle.vue';
gsap.registerPlugin(ScrollTrigger);
import aboutImg1 from '@/assets/images/about-1.webp';
import aboutImg2 from '@/assets/images/about-2.webp';
import aboutImg3 from '@/assets/images/about-3.webp';
import { i18n } from '@/locales';

const contents = computed(() => [
	{
		title: i18n.global.t('about-title-1'),
		text: i18n.global.t('about-text-1'),
		img: aboutImg1
	},
	{
		title: i18n.global.t('about-title-2'),
		text: i18n.global.t('about-text-2'),
		img: aboutImg2
	},
	{
		title: i18n.global.t('about-title-3'),
		text: i18n.global.t('about-text-3'),
		img: aboutImg3
	}
]);

const aboutRef = ref();

const scrollToAbout = () => {
	lenis.scrollTo(aboutRef.value, {
		duration: 2.5
	});
};

onMounted(() => {
	gsap.to('.about__rectangle', {
		y: '100%',
		rotate: 360,
		scrollTrigger: {
			trigger: '.about',
			start: 'top top',
			scrub: 1
		}
	});
});
</script>

<style lang="scss" scoped>
.about {
	color: var(--dark-gray);
	display: flex;
	flex-direction: column;
	gap: 10rem;

	&.active {
		.about__box {
			opacity: 1;
			transform: translate(0, 0);
		}
		.about__item {
			opacity: 1;
			transform: translateX(0);
		}
		.about__head > * {
			opacity: 1;
			transform: rotateY(0) translate(0, 0);
		}
		.about__experts {
			opacity: 1;
			transform: rotateY(0) translate(0, 0);
		}
		.about__subtitle,
		.about__text {
			opacity: 1;
			transform: translateY(0);
		}
	}
	&__list {
		list-style-type: none;
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(150px, 300px));
		justify-content: center;
		row-gap: 4rem;
	}
	&__item {
		display: flex;
		align-items: center;
		text-align: center;
		flex-direction: column;
		gap: 1rem;
		padding: 0 5rem;
		opacity: 0;
		transform: translateX(-12rem);
		transition: transform 1s, opacity 1s;
		&:not(:last-child) {
			border-right: 1px solid var(--extra-medium-gray);
			@media only screen and (max-width: 660px) {
				border-right: none;
				border-bottom: 1px solid var(--extra-medium-gray);
				padding: 4rem 1rem;
			}
		}
		&:nth-child(2) {
			transition-delay: 500ms;
		}
		&:nth-child(3) {
			transition-delay: 1s;
		}
		&-title {
			font-weight: 600;
			font-size: 18px;
		}
		&-text {
			color: var(--medium-gray);
			line-height: 30px;
			font-size: 17px;
		}
		&-img {
			margin-bottom: 30px;
			height: 10rem;
			width: 10rem;
			background-color: rgb(247, 247, 247);
			border-radius: 50%;
			display: grid;
			place-items: center;
			img {
				width: 7.5rem;
				height: 7.5rem;
				object-fit: cover;
				transform: translateY(2.5rem);
			}
		}
	}
	&__rectangle {
		position: absolute;
		inset: 0;
		width: 20rem;
		left: -10rem;
		opacity: 1;
	}
	&__subtitle {
		font-size: 18px;
		font-weight: 600;
		opacity: 0;
		transform: translateY(-20px);
		transition: transform 600ms, opacity 600ms;
	}
	&__text {
		opacity: 0;
		transform: translateY(20px);
		transition: transform 600ms, opacity 600ms;
		transition-delay: 300ms;
	}

	&__right {
		display: flex;
		flex-direction: column;
		gap: 7px;
		@media only screen and (max-width: 900px) {
			align-items: center;
			text-align: center;
		}
		p {
			font-size: 17px;
			color: #828c8a;
			font-weight: 400;
			line-height: 1.6;
		}
	}
	&__top {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		row-gap: 4rem;
		align-items: center;
		font-size: 1.9rem;
		font-weight: 500;
	}
	&__title {
		font-size: 5.5rem;
		line-height: 0.85;
		@media only screen and (max-width: 700px) {
			text-align: center;
		}
	}
	&__head {
		display: flex;
		flex-direction: column;
		gap: 3rem;
		align-items: flex-start;

		@media only screen and (max-width: 900px) {
			align-items: center;
			text-align: center;
		}
		& > * {
			opacity: 0;
			transform: rotateY(-90deg) translate(9rem, 9rem);
			transition: transform 600ms, opacity 600ms;
			&:nth-child(2) {
				transition-delay: 150ms;
			}
			&:nth-child(3) {
				transition-delay: 300ms;
			}
		}
		@media only screen and (max-width: 768px) {
			align-items: center;
			text-align: center;
		}
	}
	&__button {
		cursor: pointer;
		background: transparent;
		border: none;
		color: #fff;
		background-color: var(--dark-gray);
		padding: 1.7rem 3rem;
		border-radius: 20px;
		display: flex;
		gap: 1rem;
		transition: transform 300ms, box-shadow 300ms;
		span {
			transition: transform 300ms;
		}

		&:hover {
			transform: translateY(-5px);
			box-shadow: 0 10px 20px rgba(0, 0, 0, 0.45);
			& span {
				transform: translateX(7px);
			}
		}
		&:active {
			transform: translateY(-3px);
			box-shadow: 0 10px 20px rgba(0, 0, 0, 0.35);
		}
	}
	&__left {
		display: flex;
		flex-direction: column;
		gap: 2rem;
		&-head {
			display: flex;
			align-items: center;
			gap: 1.5rem;
		}
		@media only screen and (max-width: 700px) {
			align-items: center;
			gap: 3rem;
		}
	}

	&__icon {
		width: 2.2rem;
		height: 2.2rem;
		&-container {
			display: grid;
			place-items: center;
			background-color: var(--base-color);
			border-radius: 50%;
			width: 5.5rem;
			height: 5.5rem;
		}
	}

	&__experts {
		font-family: var(--font-base);
		display: flex;
		align-items: center;
		font-size: 17px;
		font-weight: 500;
		opacity: 0;
		transform: rotateY(-90deg) translate(9rem, 9rem);
		transition: transform 600ms, opacity 600ms;
		transition-delay: 450ms;
		overflow: hidden;

		a {
			color: inherit;
			font-weight: bold;
		}
	}
	&__left {
		font-family: var(--font-alt);
		color: var(--dark-gray);
	}
	&__ellipse {
		position: absolute;
		z-index: -1;
		top: 0;
		right: 0;
		width: 30rem;
		height: 50rem;
		@media only screen and (max-width: 800px) {
			top: 50%;
		}
	}
}
.container {
	position: relative;
	overflow: visible !important;
}
</style>
