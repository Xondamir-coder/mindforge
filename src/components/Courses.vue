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
			<li class="courses__item" v-for="content in contents" :key="content">
				<div class="courses__item-img">
					<img src="@/assets/images/about-1.webp" alt="img" />
				</div>
				<h3 class="courses__item-title">{{ content.title }}</h3>
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
import Rectangle from './Rectangle.vue';
import { i18n } from '@/locales';
import { computed } from 'vue';
gsap.registerPlugin(ScrollTrigger);

const contents = computed(() => [
	{
		title: i18n.global.t('courses-title-1'),
		text: i18n.global.t('courses-text-1'),
		link: 'https://rise.articulate.com/share/fiI3-K6KlURvjgrj4nvDOXT9d82ttZPA#/'
	},
	{
		title: i18n.global.t('courses-title-2'),
		text: i18n.global.t('courses-text-2'),
		link: 'https://rise.articulate.com/share/agirrURI99r2s6DHEW9s1Pe5z7D8guen#/lessons/CivdVBNOdHXjD6ohQfqNv1K8j544zZ7_'
	},
	{
		title: i18n.global.t('courses-title-3'),
		text: i18n.global.t('courses-text-3'),
		link: 'https://rise.articulate.com/share/9ANAJwt4wi91eLHGWxxYRGaOhfQrVW--#/'
	},
	{
		title: i18n.global.t('courses-title-4'),
		text: i18n.global.t('courses-text-4'),
		link: 'https://rise.articulate.com/share/N-uzWUbqJaxuCxiCcQGTpl5BiJP0XT-Z#/'
	},
	{
		title: i18n.global.t('courses-title-5'),
		text: i18n.global.t('courses-text-5'),
		link: 'https://rise.articulate.com/share/5kzW5bf4HlSaf_BVeFOlJavKzIv8GDt-#/'
	},
	{
		title: i18n.global.t('courses-title-6'),
		text: i18n.global.t('courses-text-6'),
		link: 'https://rise.articulate.com/share/eKfxoqO7H4T4BIgRf7vsUmJrkRPgMeyc#/'
	},
	{
		title: i18n.global.t('courses-title-7'),
		text: i18n.global.t('courses-text-7'),
		link: 'https://rise.articulate.com/share/3gOFJXXa-zUK41HWCaju8KKphQnLDsdl#/'
	},
	{
		title: i18n.global.t('courses-title-8'),
		text: i18n.global.t('courses-text-8'),
		link: 'https://rise.articulate.com/share/XaSYw9fJX8GQCFmhzzst7LyJ-UgNgIKf#/'
	},
	{
		title: i18n.global.t('courses-title-9'),
		text: i18n.global.t('courses-text-9'),
		link: 'https://rise.articulate.com/share/cbm6ZAzQhuz9OmvdrtG4zePycEs-mEiv#/'
	},
	{
		title: i18n.global.t('courses-title-10'),
		text: i18n.global.t('courses-text-10'),
		link: 'https://rise.articulate.com/share/2Ey08C-iD6zoqiJzlbDW-GYzzGgc5OcE#/'
	}
]);
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
		border: 1px solid var(--extra-medium-gray);
		border-left: none;
		border-right: none;
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
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(150px, 300px));
		grid-auto-rows: 1fr;
		justify-content: center;
	}
	&__item {
		display: flex;
		align-items: center;
		text-align: center;
		flex-direction: column;
		gap: 1rem;
		opacity: 0;
		transform: perspective(800px) rotateY(-90deg);
		transition: transform 1s, opacity 1s;
		& > *:not(.courses__container):not(.courses__item-img) {
			padding: 0 5rem;
		}
		&:not(:first-child) {
			border-left: 1px solid var(--extra-medium-gray);
		}
		@media only screen and (max-width: 660px) {
			padding: 4rem 1rem;
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
