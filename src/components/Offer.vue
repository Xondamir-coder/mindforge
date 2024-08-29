<template>
	<section class="offer section-padding">
		<div class="offer__lines"></div>
		<div class="offer__header">
			<div class="offer__header-container">
				<div class="offer__icon-container">
					<IconChat class="offer__icon" />
				</div>
				<h2 class="offer__label">{{ $t('offer-label') }}</h2>
			</div>
			<ul class="offer__list">
				<li class="offer__list-item" v-for="(button, i) in buttons" :key="button">
					<button
						class="offer__list-button"
						:class="{ active: currentIndex == i }"
						@click="changeCurIndex(i)">
						{{ button }}
					</button>
				</li>
			</ul>
		</div>
		<ul class="offer__cards">
			<li
				class="offer__card"
				v-for="(content, i) in contents"
				:key="i"
				:class="{ active: currentIndex == i }">
				<h2 class="offer__card-title">
					{{ buttons[i] }}
				</h2>
				<div class="offer__card-box">
					<img loading="lazy" :src="content.img" alt="" />
					<div class="offer__card-content">
						<p class="offer__card-text" v-for="text in content.texts" :key="text">
							{{ text }}
						</p>
						<ul class="offer__card-list">
							<li class="offer__card-item" v-for="item in content.items" :key="item">
								<p class="offer__card-text">{{ item }}</p>
							</li>
						</ul>
						<div
							class="offer__card-percentages"
							v-for="ptext in content.ptexts"
							:key="ptext">
							<span class="offer__card-percent"
								>{{ ptext.number }}{{ ptext.isNotPercent ? 'x' : '%' }}</span
							>
							<p class="offer__card-text bold">{{ ptext.text }}</p>
						</div>
					</div>
					<button class="offer__circle" @click="toggleCountdown">
						<NextCircle
							class="offer__circle-img"
							:class="[{ paused: !isCounting }, i18n.global.locale]" />
						<span>{{ countdown }}</span>
						<IconPause :class="{ hidden: isCounting }" class="offer__pause" />
					</button>
				</div>
			</li>
		</ul>
		<img ref="objRef" class="offer__obj" src="@/assets/images/offer-obj.png" alt="offer obj" />
	</section>
</template>

<script setup>
import { computed, onMounted, ref } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { i18n } from '@/locales';
import IconChat from './icons/IconChat.vue';
import offerImg1 from '@/assets/images/offer-1.webp';
import offerImg2 from '@/assets/images/offer-2.webp';
import offerImg3 from '@/assets/images/offer-3.webp';
import offerImg4 from '@/assets/images/offer-4.webp';
import NextCircle from './NextCircle.vue';
import IconPause from '@/components/icons/IconPause.vue';

gsap.registerPlugin(ScrollTrigger);

const objRef = ref();
const currentIndex = ref(0);
const countdown = ref(5);
const isCounting = ref(true);
let interval;

const buttons = computed(() => [
	i18n.global.t('offer-uni'),
	i18n.global.t('offer-school'),
	i18n.global.t('offer-corporate'),
	i18n.global.t('offer-centres')
]);
const contents = computed(() => [
	{
		img: offerImg1,
		texts: [i18n.global.t('offer-card-1-text-1'), i18n.global.t('offer-card-1-text-2')],
		ptexts: [
			{
				number: 100,
				text: i18n.global.t('offer-card-1-ptext')
			}
		],
		items: [
			i18n.global.t('offer-card-1-item-1'),
			i18n.global.t('offer-card-1-item-2'),
			i18n.global.t('offer-card-1-item-3')
		]
	},
	{
		img: offerImg2,
		texts: [i18n.global.t('offer-card-2-text-1'), i18n.global.t('offer-card-2-text-2')],
		ptexts: [
			{
				number: 100,
				text: i18n.global.t('offer-card-2-ptext')
			}
		],
		items: [
			i18n.global.t('offer-card-2-item-1'),
			i18n.global.t('offer-card-2-item-2'),
			i18n.global.t('offer-card-2-item-3')
		]
	},
	{
		img: offerImg3,
		texts: [i18n.global.t('offer-card-3-text-1'), i18n.global.t('offer-card-3-text-2')],
		ptexts: [
			{
				number: 20,
				text: i18n.global.t('offer-card-3-ptext-1')
			},
			{
				number: 80,
				text: i18n.global.t('offer-card-3-ptext-2')
			},
			{
				number: 100,
				text: i18n.global.t('offer-card-3-ptext-3')
			}
		],
		items: [
			i18n.global.t('offer-card-3-item-1'),
			i18n.global.t('offer-card-3-item-2'),
			i18n.global.t('offer-card-3-item-3')
		]
	},
	{
		img: offerImg4,
		texts: [i18n.global.t('offer-card-4-text-1'), i18n.global.t('offer-card-4-text-2')],
		ptexts: [
			{
				number: 100,
				text: i18n.global.t('offer-card-4-ptext-1')
			},
			{
				isNotPercent: true,
				number: 10,
				text: i18n.global.t('offer-card-4-ptext-2')
			}
		],
		items: [
			i18n.global.t('offer-card-4-item-1'),
			i18n.global.t('offer-card-4-item-2'),
			i18n.global.t('offer-card-4-item-3'),
			i18n.global.t('offer-card-4-item-4'),
			i18n.global.t('offer-card-4-item-5')
		]
	}
]);

const changeCurIndex = i => {
	currentIndex.value = i;
	countdown.value = 5;
};
const setCountdown = () => {
	interval = setInterval(() => {
		countdown.value--;
		if (countdown.value < 0) {
			currentIndex.value = (currentIndex.value + 1) % 4;
			countdown.value = 5;
		}
	}, 1000);
};
const toggleCountdown = () => {
	isCounting.value = !isCounting.value;
	if (isCounting.value) {
		setCountdown();
	} else {
		clearInterval(interval);
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

	setCountdown();
});
</script>

<style lang="scss" scoped>
@keyframes rotate {
	from {
		transform: rotate(0deg);
	}
	to {
		transform: rotate(360deg);
	}
}

ul {
	list-style: none;
}
button {
	background-color: transparent;
	border: none;
	color: inherit;
}
.offer {
	color: #fff;
	background-image: linear-gradient(to right bottom, #154c79, #0f3757, #0d2c43, #0b1e31, #091227);
	position: relative;
	display: flex;
	gap: 3rem;
	flex-direction: column;
	padding-left: 3vw;
	padding-right: 3vw;
	transform-style: preserve-3d;

	.offer__pause {
		width: 3.2rem;
		height: 3.2rem;
		transform: translateY(5px) scale(1);
		transition: transform 300ms;
		&.hidden {
			transform: translateY(5px) scale(0);
		}
	}

	&__circle {
		align-self: end;
		display: grid;
		place-items: center;
		& > * {
			grid-row: 1 / span 1;
			grid-column: 1 / span 1;
		}

		&-img {
			animation: rotate 5s infinite linear;
			transform-origin: 50% 64%;
			&.paused {
				animation-play-state: paused;
			}
		}

		span {
			transition: transform 300ms;
			transform: translateY(5px);
			font-size: 2.4rem;
			font-weight: 700;
			transform: translateY(5px) scale(0);
			&:has(+ .offer__pause.hidden) {
				transform: translateY(5px) scale(1);
			}
		}
	}
	&__cards {
		display: grid;
		padding: 1rem 5vw;
		@media only screen and (max-width: 900px) {
			padding: 1rem 0;
		}
	}
	&__card {
		grid-column: 1 / span 1;
		grid-row: 1 / span 1;
		display: flex;
		flex-direction: column;
		gap: 3.6rem;
		padding: 6rem;
		background-color: #fff;
		border-radius: 16px;
		color: #000;
		z-index: 1;
		line-height: 2.4rem;

		// 1-animation

		// transition: transform 1s, border-radius 1s, opacity 0.5s;
		// transform: scale(0.8);
		// border-radius: 50%;
		// opacity: 0;
		// @media only screen and (max-width: 900px) {
		// 	border-radius: 30%;
		// }
		// &.active {
		// 	transform: scale(1);
		// 	border-radius: 16px;
		// 	opacity: 1;
		// 	z-index: 10;
		// }

		// 2-animation

		// transform: perspective(1000px) rotateX(45deg) scale(0.9);
		// transition: transform 1.2s cubic-bezier(0.77, 0, 0.175, 1), opacity 1.2s;
		// opacity: 0;
		// &.active {
		// 	transform: perspective(1000px) rotateX(0) scale(1);
		// 	opacity: 1;
		// 	z-index: 10;
		// }

		// 2.5-animation
		transform-origin: right bottom; /* Origin point for peeling effect */
		transform: perspective(1000px) rotateX(20deg) rotateY(-30deg) rotateZ(-10deg) scale(1);
		transition: transform 1.2s cubic-bezier(0.77, 0, 0.175, 1), opacity 1.2s;
		opacity: 0;
		&.active {
			transform: perspective(1000px) rotateX(0) rotateY(0) rotateZ(0) scale(1);
			opacity: 1;
		}

		// 3-animation

		// transition: transform 2s ease, clip-path 2s ease, opacity 2s;
		// transform: scale(1);
		// clip-path: circle(0% at 50% 50%);
		// opacity: 0;
		// &.active {
		// 	transform: scale(1);
		// 	clip-path: circle(100% at 50% 50%);
		// 	opacity: 1;
		// 	z-index: 10;
		// }

		@media only screen and (max-width: 900px) {
			padding: 2rem;
		}
		&-title {
			font-size: 2.4rem;
			font-weight: 600;
		}
		&-content {
			flex: 1;
			display: flex;
			flex-direction: column;
			gap: 1.6rem;
		}
		&-list {
			list-style: initial;
			margin-left: 2.5rem;
			display: flex;
			flex-wrap: wrap;
			flex-direction: column;
			gap: 5px;
		}
		&-percentages {
			display: grid;
			grid-template-columns: 80px 1fr;
			align-items: center;
			span {
				padding-right: 1.6rem;
				border-right: 1px solid #000;
				font-size: 2.6rem;
				font-weight: bold;
				font-family: var(--font-alt);
				text-align: center;
			}
			p {
				padding-left: 1.6rem;
			}
		}
		&-text {
			font-size: 1.6rem;
			font-weight: 500;
			&.bold {
				font-weight: 600;
			}
		}
		&-box {
			flex-grow: 1;
			display: flex;
			justify-content: stretch;
			flex-wrap: wrap;
			gap: 4rem;
			@media only screen and (max-width: 600px) {
				flex-direction: column;
			}
		}
		img {
			align-self: center;
			flex: 1;
			width: 100%;
			height: 100%;
			min-width: 250px;
			border-radius: 16px;
			object-fit: cover;
		}
	}
	&__list {
		display: flex;
		flex-wrap: wrap;
		gap: 2rem;
		&-item {
			font-size: 2rem;
			width: fit-content;
		}
		&-button {
			padding: 10px 0;
			position: relative;
			&::before {
				content: '';
				width: 100%;
				height: 3px;
				position: absolute;
				background-color: #fff;
				bottom: 0;
				transition: width 300ms;
				width: 0;
				left: 0;
			}
			&.active::before {
				width: 100%;
			}
		}
	}
	&__label {
		font-size: 2.4rem;
		font-weight: 400;
	}

	&__header {
		z-index: 1;
		display: flex;
		gap: 2rem;
		flex-wrap: wrap;
		align-items: center;
		justify-content: space-between;
		&-container {
			display: flex;
			align-items: center;
			gap: 15px;
		}
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
