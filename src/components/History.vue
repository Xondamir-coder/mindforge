<template>
	<section class="history section-padding" ref="historyRef">
		<div class="history__head">
			<p class="history__label">{{ $t('history-label') }}</p>
			<h1 class="history__title">{{ $t('history-title') }}</h1>
		</div>
		<ul class="history__list">
			<li class="history__item" v-for="content in contents" :key="content.title">
				<p class="history__item-date">{{ content.date }}</p>
				<h2 class="history__item-title">{{ content.title }}</h2>
				<p class="history__item-text">{{ content.text }}</p>
			</li>
		</ul>
	</section>
</template>

<script setup>
import { i18n } from '@/locales';
import { computed } from 'vue';

const contents = computed(() => [
	{
		title: i18n.global.t('history-title-1'),
		text: i18n.global.t('history-text-1'),
		date: i18n.global.t('history-date-1')
	},
	{
		title: i18n.global.t('history-title-2'),
		text: i18n.global.t('history-text-2'),
		date: i18n.global.t('history-date-2')
	},
	{
		title: i18n.global.t('history-title-3'),
		text: i18n.global.t('history-text-3'),
		date: i18n.global.t('history-date-3')
	},
	{
		title: i18n.global.t('history-title-4'),
		text: i18n.global.t('history-text-4'),
		date: i18n.global.t('history-date-4')
	},
	{
		title: i18n.global.t('history-title-5'),
		text: i18n.global.t('history-text-5'),
		date: i18n.global.t('history-date-5')
	},
	{
		title: i18n.global.t('history-title-6'),
		text: i18n.global.t('history-text-6'),
		date: i18n.global.t('history-date-6')
	},
	{
		title: i18n.global.t('history-title-7'),
		text: i18n.global.t('history-text-7'),
		date: i18n.global.t('history-date-7')
	},
	{
		title: i18n.global.t('history-title-8'),
		text: i18n.global.t('history-text-8'),
		date: i18n.global.t('history-date-8')
	}
]);
</script>

<style lang="scss" scoped>
.history {
	display: flex;
	flex-direction: column;
	gap: 6rem;
	color: var(--dark-gray);
	overflow: hidden;
	&.active &__head {
		opacity: 1;
		transform: rotateY(0) translate(0, 0);
	}
	&.active &__list {
		transform: perspective(800px) rotateX(0) translateZ(0);
	}
	&__list {
		list-style: none;
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		row-gap: 4rem;
		transform-style: preserve-3d;
		transform: perspective(800px) rotateX(33deg) translateZ(75px);
		transition: transform 1.5s;
	}
	&__item {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 10px;
		padding: 25%;
		border: 1px solid var(--extra-medium-gray);
		position: relative;
		transition: background-color 400ms, color 400ms;
		&:hover {
			background-color: var(--dark-gray);
			color: #fff;
		}
		&-date {
			position: absolute;
			top: 3rem;
			right: 3rem;
			font-size: 17px;
			font-weight: bold;
		}
		&-title {
			font-size: 18px;
		}
		&-text {
			font-size: 16px;
		}
	}
	&__head {
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 1.5rem;
		text-align: center;
		color: var(--dark-gray);
	}
	&__title {
		font-size: 4.8rem;
		font-weight: 700;
	}
	&__label {
		font-size: 16px;
		font-weight: 600;
	}
}
</style>
