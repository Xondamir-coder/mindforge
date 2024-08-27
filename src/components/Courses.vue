<template>
	<section class="courses section-padding">
		<div class="courses__top">
			<div class="courses__left">
				<div class="courses__head">
					<div class="courses__top">
						<div class="courses__icon-container">
							<IconAward class="courses__icon" />
						</div>
						<span>{{ $t('courses-label') }}</span>
					</div>
					<h1 class="courses__title">{{ $t('courses-title') }}</h1>
				</div>
			</div>
			<div class="courses__right">
				<h2 class="courses__subtitle">{{ $t('courses-subtitle') }}</h2>
				<p class="courses__text">
					{{ $t('courses-text') }}
				</p>
			</div>
		</div>
		<ul class="courses__list">
			<li
				class="courses__item"
				v-for="(content, index) in contents"
				:key="content"
				:class="{ 'no-border': rightmostIndexes.includes(index) }">
				<div class="courses__item-img">
					<img src="@/assets/images/about-1.webp" alt="img" />
				</div>
				<h3 class="courses__item-title">{{ content.title.toLowerCase() }}</h3>
				<p class="courses__item-text">{{ content.text }}</p>
				<div class="courses__container">
					<p>&ThinSpace;</p>
					<a :href="content.link" target="_blank" class="courses__button">
						{{ $t('go-to') }}
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="16"
							height="16"
							fill="currentColor"
							viewBox="0 0 16 16">
							<path
								fill-rule="evenodd"
								d="M1 8a.5.5 0 0 1 .5-.5h11.793l-3.147-3.146a.5.5 0 0 1 .708-.708l4 4a.5.5 0 0 1 0 .708l-4 4a.5.5 0 0 1-.708-.708L13.293 8.5H1.5A.5.5 0 0 1 1 8" />
						</svg>
					</a>
				</div>
			</li>
		</ul>
	</section>
</template>

<script setup>
import IconAward from './icons/IconAward.vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { i18n } from '@/locales';
import { computed, onMounted, onUnmounted, ref } from 'vue';
gsap.registerPlugin(ScrollTrigger);

const contents = computed(() => [
	{
		title: i18n.global.t('courses-title-1'),
		text: i18n.global.t('courses-text-1'),
		link: '/critical-thinking'
	},
	{
		title: i18n.global.t('courses-title-2'),
		text: i18n.global.t('courses-text-2'),
		link: '/english'
	},
	{
		title: i18n.global.t('courses-title-3'),
		text: i18n.global.t('courses-text-3'),
		link: '/maths'
	},
	{
		title: i18n.global.t('courses-title-4'),
		text: i18n.global.t('courses-text-4'),
		link: '/business-com'
	},
	{
		title: i18n.global.t('courses-title-5'),
		text: i18n.global.t('courses-text-5'),
		link: '/business-ethics'
	},
	{
		title: i18n.global.t('courses-title-6'),
		text: i18n.global.t('courses-text-6'),
		link: '/hrm'
	},
	{
		title: i18n.global.t('courses-title-7'),
		text: i18n.global.t('courses-text-7'),
		link:
			i18n.global.locale == 'uz'
				? 'consumer-behavior-ru'
				: `consumer-behavior-${i18n.global.locale}`
	},
	{
		title: i18n.global.t('courses-title-8'),
		text: i18n.global.t('courses-text-8'),
		link: i18n.global.locale == 'uz' ? 'statistics-ru' : `statistics-${i18n.global.locale}`
	},
	{
		title: i18n.global.t('courses-title-9'),
		text: i18n.global.t('courses-text-9'),
		link: '/organizational-behaviour'
	},
	{
		title: i18n.global.t('courses-title-10'),
		text: i18n.global.t('courses-text-10'),
		link: '/performance-management'
	}
	//PRESENTATION SKILLS NOT ADDED
]);

const rightmostIndexes = ref([]);

const updateRightmostItems = () => {
	const items = document.querySelectorAll('.courses__item');
	let previousTopOffset = items[0].offsetTop;

	items.forEach((item, index) => {
		const currentTopOffset = item.offsetTop;

		// Detect if this item starts a new row
		if (currentTopOffset !== previousTopOffset) {
			rightmostIndexes.value.push(index - 1); // Mark the previous item as the rightmost
			previousTopOffset = currentTopOffset;
		}
	});

	// Ensure the last item in the list is marked if it's the rightmost
	rightmostIndexes.value.push(items.length - 1);
};

onMounted(() => {
	updateRightmostItems();

	// Optional: add resize event listener to handle screen size changes
	window.addEventListener('resize', updateRightmostItems);
});
onUnmounted(() => {
	window.removeEventListener('resize', updateRightmostItems);
});
</script>

<style lang="scss" scoped>
.courses {
	color: var(--dark-gray);
	overflow: hidden;
	display: flex;
	flex-direction: column;
	gap: 10rem;
	transform-style: preserve-3d;

	&.active {
		.courses__box {
			opacity: 1;
			transform: translate(0, 0);
		}
		.courses__item {
			opacity: 1;
			transform: perspective(800px) rotateY(0);
		}
		.courses__head > * {
			opacity: 1;
			transform: rotateY(0) translate(0, 0);
		}
		.courses__experts {
			opacity: 1;
			transform: rotateY(0) translate(0, 0);
		}
		.courses__subtitle,
		.courses__text {
			opacity: 1;
			transform: translateY(0);
		}
	}
	&__container {
		align-self: stretch;
		font-size: 16px;
		font-weight: bold;
		display: flex;
		flex-direction: column;
		margin-top: auto;
		border-top: 1px solid var(--extra-medium-gray);
		border-bottom: 1px solid var(--extra-medium-gray);
		position: relative;
		overflow: hidden;
		p {
			padding: 1.5rem;
			transition: transform 0.5s;
		}
		a {
			transition: top 0.5s;
			position: absolute;
			width: 100%;
			height: 100%;
			left: 0;
			top: 100%;
			color: #fff;
			background-color: var(--dark-gray);
			padding: 1.5rem;
			text-decoration: none;
			display: flex;
			align-items: center;
			gap: 10px;
			justify-content: center;
			font-weight: 400;
			letter-spacing: 0.3px;
			svg {
				transition: transform 300ms;
			}
			&:hover svg {
				transform: translateX(7px);
			}
		}
	}
	&__list {
		list-style-type: none;
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}
	&__item {
		flex: 1;
		max-width: 300px;
		min-width: 300px;
		display: flex;
		align-items: center;
		text-align: center;
		flex-direction: column;
		gap: 1rem;
		opacity: 0;
		transform: perspective(800px) rotateY(-90deg);
		transition: transform 1s, opacity 1s;
		&.no-border {
			border-right: none !important;
		}

		&:not(:last-child) {
			border-right: 1px solid var(--extra-medium-gray);
		}
		& > *:not(.courses__container):not(.courses__item-img) {
			padding: 0 5rem;
		}
		&:nth-child(6) {
			.courses__item-title {
				text-transform: uppercase;
			}
		}
		@media only screen and (max-width: 660px) {
			padding: 1rem;
			padding-bottom: 2rem;
			border-right: none !important;
		}
		@for $index from 1 through 10 {
			&:nth-child(#{$index}) {
				transition-delay: $index * 0.2s;
			}
		}
		&:hover .courses__container {
			a {
				top: 0;
			}
			p {
				transform: translateY(15px);
			}
		}
		&-title {
			font-weight: 600;
			font-size: 18px;
			&::first-letter {
				text-transform: uppercase;
			}
		}
		&-text {
			color: var(--medium-gray);
			line-height: 24px;
			font-size: 17px;
		}
		&-img {
			margin-top: 2rem;
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
		align-self: end;
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
		display: flex;
		align-items: center;
		gap: 30px;
		font-size: 1.9rem;
		font-weight: 500;
		@media only screen and (max-width: 900px) {
			flex-direction: column;
		}
	}
	&__title {
		font-size: 5.5rem;
		line-height: 0.85;
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

	&__left {
		display: flex;
		flex-direction: column;
		grid-area: left;
		gap: 8rem;

		@media only screen and (max-width: 768px) {
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
	&__left {
		font-family: var(--font-alt);
		color: var(--dark-gray);
	}
}
</style>
