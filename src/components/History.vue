<template>
	<section class="history section-padding" ref="historyRef">
		<div class="history__head">
			<p class="history__label">Наша история</p>
			<h1 class="history__title">Предоставляем 6 лет верной услуги</h1>
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
const contents = [
	{
		title: 'Уроков',
		text: '1300+',
		date: '2018'
	},
	{
		title: 'Предметов',
		text: '65+',
		date: '2019'
	},
	{
		title: 'Страниц',
		text: '295,000+',
		date: '2020'
	},
	{
		title: 'Чтения',
		text: '10,400+ часов',
		date: '2021'
	},
	{
		title: 'Направлений',
		text: '14+',
		date: '2022'
	},
	{
		title: 'Создание',
		text: '5200+ часов',
		date: '2023'
	},
	{
		title: 'Пользователей',
		text: '24,000+',
		date: '2024'
	},
	{
		title: 'Видеоуроков',
		text: '700+ часов',
		date: '2024'
	}
];
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
