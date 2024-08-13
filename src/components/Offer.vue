<template>
	<section class="offer section-padding">
		<div class="offer__lines"></div>
		<img ref="objRef" class="offer__obj" src="@/assets/images/offer-obj.png" alt="offer obj" />
		<div class="offer__left">
			<div class="offer__top">
				<div class="offer__icon-container">
					<IconChat class="offer__icon" />
				</div>
				<span>Students feedback</span>
			</div>
			<h1 class="offer__title">Trusted by genius people.</h1>
			<p class="offer__text">
				Lorem ipsum dolor sit amet consectetur adipiscing elit venenatis dictum nec.
			</p>
			<div class="offer__content">
				<h2 class="offer__content-data">99%</h2>
				<div class="offer__content-divider"></div>
				<div class="offer__content-text">Student's complete course successfully.</div>
			</div>
		</div>
		<div class="offer__right">
			<button class="offer__button" @click="changeCurSlide('prev')">
				<IconLess class="offer__button-icon" />
			</button>
			<button class="offer__button" @click="changeCurSlide('next')">
				<IconGreater class="offer__button-icon" />
			</button>
			<div class="offer__container">
				<div
					class="offer__box"
					v-for="(content, index) in contents"
					:key="content.name"
					:style="{
						transform: `translateX(calc(${(index - curSlide) * 100}% + ${
							(index - curSlide) * 50
						}px))`
					}">
					<img class="offer__box-img" :src="content.img" alt="img" />
					<div class="offer__box-content">
						<div class="offer__stars">
							<svg
								v-for="i in [1, 2, 3, 4, 5]"
								:key="i"
								xmlns="http://www.w3.org/2000/svg"
								width="16"
								height="16"
								fill="#fff"
								class="bi bi-star-fill"
								viewBox="0 0 16 16">
								<path
									d="M3.612 15.443c-.386.198-.824-.149-.746-.592l.83-4.73L.173 6.765c-.329-.314-.158-.888.283-.95l4.898-.696L7.538.792c.197-.39.73-.39.927 0l2.184 4.327 4.898.696c.441.062.612.636.282.95l-3.522 3.356.83 4.73c.078.443-.36.79-.746.592L8 13.187l-4.389 2.256z" />
							</svg>
						</div>
						<p class="offer__box-text">{{ content.text }}</p>
						<h2 class="offer__box-name">{{ content.name }}</h2>
						<h3 class="offer__box-job">{{ content.job }}</h3>
					</div>
				</div>
			</div>
		</div>
	</section>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import IconChat from './icons/IconChat.vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);
import offerImg1 from '@/assets/images/offer-1.jpg';
import offerImg2 from '@/assets/images/offer-2.jpg';
import offerImg3 from '@/assets/images/offer-3.jpg';
import IconLess from './icons/IconLess.vue';
import IconGreater from './icons/IconGreater.vue';

const objRef = ref();
const curSlide = ref(0);
const contents = [
	{
		img: offerImg1,
		text: 'Course materials were good, the mentoring approach was good and working with other people via the internet was good.',
		name: 'Aizen Sosuke',
		job: 'Traitor'
	},
	{
		img: offerImg2,
		text: 'Course materials were good, the mentoring approach was good and working with other people via the internet was good.',
		name: 'Shunsui Kyoraku',
		job: 'Head Commander'
	},
	{
		img: offerImg3,
		text: 'Course materials were good, the mentoring approach was good and working with other people via the internet was good.',
		name: 'Yhwach',
		job: 'King of Wandenreich'
	}
];

const changeCurSlide = direction => {
	if (direction === 'next') {
		curSlide.value = curSlide.value === contents.length - 1 ? 0 : curSlide.value + 1;
	} else {
		curSlide.value = curSlide.value === 0 ? contents.length - 1 : curSlide.value - 1;
	}
};

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
	display: grid;
	grid-auto-columns: 1fr 1.5fr;
	grid-template-areas: 'left right';
	gap: 10rem;
	overflow: hidden;
	padding-top: 15rem;
	padding-bottom: 15rem;

	&.active &__left > *:not(.offer__text) {
		opacity: 1;
		transform: rotateY(0) translate(0, 0);
	}
	&.active &__text {
		opacity: 0.4;
		transform: rotateY(0) translate(0, 0);
	}
	&.active &__button {
		scale: 1;
	}
	@media only screen and (max-width: 1300px) {
		grid-auto-columns: initial;
		grid-template-areas:
			'left'
			'right';
		grid-auto-rows: 1fr 1.5fr;
	}
	@media only screen and (max-width: 600px) {
		grid-auto-rows: 1fr 2fr;
	}
	&__container {
		overflow: hidden;
		width: 100%;
		position: relative;
	}
	&__left {
		grid-area: left;
		position: relative;
		z-index: 1;
		display: flex;
		flex-direction: column;
		gap: 30px;
		font-family: var(--font-alt);
		& > * {
			opacity: 0;
			transform: rotateY(-100deg) translate(9rem, 9rem);
			transition: opacity 800ms, transform 800ms;
		}
	}
	&__right {
		grid-area: right;
		position: relative;
		z-index: 1;
		display: flex;
	}
	&__button {
		border: none;
		background-color: transparent;
		width: 4.5rem;
		height: 4.5rem;
		position: absolute;
		z-index: 2;
		border-radius: 50%;
		display: grid;
		place-items: center;
		background-color: #fff;
		top: 50%;
		transform: translate(-50%, -50%);
		box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
		scale: 0;
		transition: scale 300ms;
		transition-delay: 0.5s;
		&:first-of-type {
			left: 0;
		}
		&:last-of-type {
			left: 100%;
			transition-delay: 0.8s;
		}
		&-icon {
			fill: var(--dark-gray);
			width: 50%;
			height: 50%;
		}
	}
	&__box {
		position: absolute;
		inset: 0;
		color: var(--medium-gray);
		background-color: #fff;
		border-radius: 10px;
		transition: transform 1s;
		display: grid;
		grid-template-columns: 1fr 1.5fr;
		@media only screen and (max-width: 600px) {
			grid-template-columns: initial;
			grid-template-rows: 40rem 1fr;
		}
		&-img {
			object-fit: cover;
			border-top-left-radius: 10px;
			border-bottom-left-radius: 10px;
			height: 100%;
			width: 100%;
		}
		&-text {
			line-height: 30px;
			font-size: 17px;
		}
		&-name {
			font-size: 18px;
			font-weight: 600;
			color: var(--dark-gray);
		}
		&-job {
			font-size: 16px;
			font-weight: 400;
			margin-top: -1rem;
		}
		&-content {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: start;
			gap: 2rem;
			padding: 6rem;
		}
	}
	&__stars {
		padding: 1rem 2rem;
		display: flex;
		justify-content: start;
		gap: 3px;
		background-color: #ef991f;
		border-radius: 50px;
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
