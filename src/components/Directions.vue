<template>
	<section class="directions section-padding">
		<h1 class="directions__title">
			{{ $t('directions-title') }}
		</h1>
		<ul class="directions__list">
			<li class="directions__item" v-for="content in contents" :key="content">
				<div class="directions__container">
					<img :src="content.img" class="directions__img" alt="img" />
					<div class="directions__container-gradient"></div>
					<div class="directions__item-data">
						<p class="directions__text" v-for="data in content.data" :key="data">
							{{ data }}
						</p>
					</div>
				</div>
				<h2 class="directions__item-title">{{ content.title }}</h2>
			</li>
		</ul>
	</section>
</template>

<script setup>
import directionsImg1 from '@/assets/images/directions-1.jpg';
import directionsImg2 from '@/assets/images/directions-2.jpg';
import directionsImg3 from '@/assets/images/directions-3.jpg';
import directionsImg4 from '@/assets/images/directions-4.jpg';
import directionsImg5 from '@/assets/images/directions-5.jpg';
import directionsImg6 from '@/assets/images/directions-6.jpg';
import directionsImg7 from '@/assets/images/directions-7.jpg';
import directionsImg8 from '@/assets/images/directions-8.jpg';
import directionsImg10 from '@/assets/images/directions-10.jpg';
import directionsImg11 from '@/assets/images/directions-11.jpg';
import { computed } from 'vue';
import { i18n } from '@/locales';

const contents = computed(() => [
	{
		title: i18n.global.t('directions-title-1'),
		img: directionsImg1,
		data: [
			i18n.global.t('directions-data-1-text-1'),
			i18n.global.t('directions-data-1-text-2'),
			i18n.global.t('directions-data-1-text-3'),
			i18n.global.t('directions-data-1-text-4'),
			i18n.global.t('directions-data-1-text-5'),
			i18n.global.t('directions-data-1-text-6')
		]
	},
	{
		title: i18n.global.t('directions-title-2'),
		img: directionsImg2,
		data: [
			i18n.global.t('directions-data-2-text-1'),
			i18n.global.t('directions-data-2-text-2'),
			i18n.global.t('directions-data-2-text-3'),
			i18n.global.t('directions-data-2-text-4'),
			i18n.global.t('directions-data-2-text-5'),
			i18n.global.t('directions-data-2-text-6')
		]
	},
	{
		title: i18n.global.t('directions-title-3'),
		img: directionsImg3,
		data: [
			i18n.global.t('directions-data-3-text-1'),
			i18n.global.t('directions-data-3-text-2'),
			i18n.global.t('directions-data-3-text-3'),
			i18n.global.t('directions-data-3-text-4'),
			i18n.global.t('directions-data-3-text-5'),
			i18n.global.t('directions-data-3-text-6')
		]
	},
	{
		title: i18n.global.t('directions-title-4'),
		img: directionsImg4,
		data: [
			i18n.global.t('directions-data-4-text-1'),
			i18n.global.t('directions-data-4-text-2'),
			i18n.global.t('directions-data-4-text-3'),
			i18n.global.t('directions-data-4-text-4'),
			i18n.global.t('directions-data-4-text-5'),
			i18n.global.t('directions-data-4-text-6')
		]
	},
	{
		title: i18n.global.t('directions-title-5'),
		img: directionsImg5,
		data: [
			i18n.global.t('directions-data-5-text-1'),
			i18n.global.t('directions-data-5-text-2'),
			i18n.global.t('directions-data-5-text-3'),
			i18n.global.t('directions-data-5-text-4'),
			i18n.global.t('directions-data-5-text-5'),
			i18n.global.t('directions-data-5-text-6')
		]
	},
	{
		title: i18n.global.t('directions-title-6'),
		img: directionsImg6,
		data: [
			i18n.global.t('directions-data-6-text-1'),
			i18n.global.t('directions-data-6-text-2'),
			i18n.global.t('directions-data-6-text-3'),
			i18n.global.t('directions-data-6-text-4'),
			i18n.global.t('directions-data-6-text-5')
		]
	},
	{
		title: i18n.global.t('directions-title-7'),
		img: directionsImg7,
		data: [
			i18n.global.t('directions-data-7-text-1'),
			i18n.global.t('directions-data-7-text-2'),
			i18n.global.t('directions-data-7-text-3'),
			i18n.global.t('directions-data-7-text-4'),
			i18n.global.t('directions-data-7-text-5')
		]
	},
	{
		title: i18n.global.t('directions-title-8'),
		img: directionsImg8,
		data: [
			i18n.global.t('directions-data-8-text-1'),
			i18n.global.t('directions-data-8-text-2'),
			i18n.global.t('directions-data-8-text-3'),
			i18n.global.t('directions-data-8-text-4'),
			i18n.global.t('directions-data-8-text-5'),
			i18n.global.t('directions-data-8-text-6')
		]
	},
	{
		title: i18n.global.t('directions-title-9'),
		img: directionsImg10,
		data: [
			i18n.global.t('directions-data-9-text-1'),
			i18n.global.t('directions-data-9-text-2'),
			i18n.global.t('directions-data-9-text-3'),
			i18n.global.t('directions-data-9-text-4')
		]
	},
	{
		title: i18n.global.t('directions-title-10'),
		img: directionsImg11,
		data: [
			i18n.global.t('directions-data-10-text-1'),
			i18n.global.t('directions-data-10-text-2'),
			i18n.global.t('directions-data-10-text-3'),
			i18n.global.t('directions-data-10-text-4'),
			i18n.global.t('directions-data-10-text-5'),
			i18n.global.t('directions-data-10-text-6')
		]
	}
]);
</script>

<style lang="scss" scoped>
.directions {
	display: flex;
	flex-direction: column;
	gap: 7rem;
	&.active &__item {
		opacity: 1;
		transform: perspective(800px) rotateX(0) translateZ(0);
	}
	&__img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		position: absolute;
		inset: 0;
		z-index: -1;
	}
	&__title {
		text-align: center;
		font-size: 4.8rem;
		font-weight: 700;
	}
	&__list {
		display: flex;
		justify-content: center;
		flex-wrap: wrap;
		list-style: none;
		column-gap: 3rem;
		row-gap: 6rem;
		& > * {
			max-width: 38rem;
			min-width: 38rem;
			flex: 1;
			@media only screen and (max-width: 700px) {
				flex-basis: 100%;
				max-width: 100%;
			}
		}
	}
	&__container {
		position: relative;
		border-radius: 10px;
		overflow: hidden;
		&-gradient {
			position: absolute;
			inset: 0;
			background: linear-gradient(to top, #262a29 0%, transparent 100%);
			width: 100%;
			height: 100%;
			opacity: 0;
			transition: opacity 400ms;
		}
	}
	&__text {
		font-size: 1.8rem;
		opacity: 0;
		transform: translateY(4rem);
		transition: opacity 400ms, transform 400ms;
	}
	&__item {
		display: grid;
		grid-template-rows: 300px max-content;
		gap: 1.5rem;
		transform: perspective(800px) rotateX(40deg) translateZ(100px);
		transition: transform 1s, opacity 1s;
		opacity: 0;
		@for $i from 1 through 10 {
			&:nth-child(#{$i}) {
				transition-delay: $i * 0.2s;
			}
		}
		&:hover .directions__text {
			opacity: 1;
			transform: translateY(0);
		}
		&:hover .directions__container-gradient {
			opacity: 1;
		}
		&:hover &-data {
			overflow-y: auto;
		}

		&-data {
			height: 100%;
			display: flex;
			flex-direction: column;
			gap: 10px;
			padding: 25px;
			color: #fff;
			line-height: 1.5;
			position: relative;
		}
		&-title {
			font-size: 2.6rem;
		}
	}
}
</style>
