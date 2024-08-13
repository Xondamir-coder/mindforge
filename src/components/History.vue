<template>
	<section class="history section-padding" ref="historyRef">
		<div class="history__head">
			<p class="history__label">Наша история</p>
			<h1 class="history__title">Предоставляем 6 лет верной услуги</h1>
			<p class="history__text">
				Mindforge — молодая и динамичная компания, создающая обучающий контент с 2018 года.
				Наша команда превращает свои знания в качественные и запоминающиеся материалы для
				ваших нужд.
			</p>
		</div>
		<div class="history__content">
			<div class="history__bar"></div>
			<div class="history__box" v-for="content in history" :key="content.date">
				<div class="history__box-left">
					<h2 class="history__box-title">{{ content.date }}</h2>
					<h3 class="history__box-subtitle">{{ content.title }}</h3>
				</div>
				<div class="history__box-middle">
					<div class="history__circle"></div>
				</div>
				<div class="history__box-right">
					<p class="history__box-desc">{{ content.desc }}</p>
				</div>
			</div>
		</div>
	</section>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const history = [
	{
		date: '2018',
		title: 'Основание компании',
		desc: 'Mindforge начала свою деятельность в 2018 году, сосредоточив усилия на создании качественного обучающего контента. Наша команда с первых дней была полна энтузиазма и приверженности делу.'
	},
	{
		date: '2019',
		title: 'Укрепление бизнеса и уверенность',
		desc: 'Mindforge стабилизировала свои процессы и обрела уверенность в создании эффективного и востребованного образовательного контента. Мы продолжали развивать наши навыки и расширять спектр услуг.'
	},
	{
		date: '2020',
		title: 'Расширение портфолио проектов',
		desc: 'Mindforge успешно увеличила количество проектов и заказчиков, закрепив свою репутацию надежного партнера в сфере разработки онлайн-контента.'
	},
	{
		date: '2021',
		title: 'Укрепление бренда и привлечение клиентов',
		desc: 'Mindforge укрепила свой бренд, став синонимом качества и инноваций в создании образовательного контента. Мы привлекли новых клиентов и создали лояльную базу пользователей.'
	},
	{
		date: '2022',
		title: 'Внедрение новых услуг и продуктов',
		desc: 'Mindforge продолжила внедрять новые услуги и продукты, расширяя возможности для создания уникального контента и предоставления разнообразных обучающих решений для клиентов.'
	},
	{
		date: '2023',
		title: 'Расширение на международные рынки',
		desc: 'Mindforge вышла на международные рынки, предоставляя свои услуги по созданию онлайн-контента клиентам по всему миру. Наша экспертиза и качество привлекли новых партнеров и проекты.'
	},
	{
		date: '2024',
		title: 'Инновации и дальнейший рост',
		desc: 'В 2024 году Mindforge продолжает внедрять инновации в сфере онлайн-образования, расширяя свой портфель и предлагая новые решения для еще большего охвата аудитории.'
	}
];

const historyRef = ref();

onMounted(() => {
	const handler = entries => {
		entries.forEach(entry => {
			if (entry.isIntersecting) {
				entry.target.classList.add('active');
			} else {
				entry.target.classList.remove('active');
			}
		});
	};
	const observer = new IntersectionObserver(handler, { threshold: 0.9 });
	historyRef.value.querySelectorAll('.history__box').forEach(box => observer.observe(box));
});
</script>

<style lang="scss" scoped>
.history {
	display: flex;
	flex-direction: column;
	gap: max(8rem, 10vw);
	color: var(--dark-gray);
	&.active &__head {
		opacity: 1;
		transform: rotateY(0) translate(0, 0);
	}
	&__box {
		font-weight: 700;
		display: grid;
		align-self: start;
		grid-template-columns: 1fr 19.2rem 1fr;
		height: 100%;
		grid-template-areas: 'left middle right';
		@media only screen and (max-width: 800px) {
			grid-template-columns: initial;
			gap: 4rem;
			grid-template-areas:
				'middle left'
				'middle right';
			row-gap: 2rem;
		}
		& > *:not(.history__box-middle) {
			transition: opacity 600ms;
			opacity: 0.5;
		}
		&.active > * {
			opacity: 1;
		}
		&.active .history__circle {
			box-shadow: 0 0 0 8px var(--dark-gray);
		}
		&-right {
			grid-area: right;
		}
		&-left {
			display: flex;
			flex-direction: column;
			gap: 1rem;
			grid-area: left;
		}
		&-middle {
			grid-area: middle;
			display: grid;
			justify-items: center;
		}
		&-title {
			font-size: 4rem;
		}
		&-subtitle {
			font-size: 3.2rem;
		}
		&-desc {
			font-size: 18px;
			font-weight: 400;
			letter-spacing: 0.2px;
			line-height: 1.7;
		}
	}
	&__content {
		position: relative;
		display: grid;
		place-items: center;
		grid-auto-rows: 20rem;
		gap: 5vw;
		@media only screen and (max-width: 800px) {
			grid-auto-rows: 1fr;
			gap: 10rem;
		}
	}
	&__circle {
		border-radius: 100%;
		width: 1.5rem;
		height: 1.5rem;
		position: sticky;
		top: 50vh;
		box-shadow: 0 0 0 8px #a4b4af;
		background-color: #fff;
		transition: box-shadow 600ms;
	}
	&__bar {
		background-color: var(--dark-gray);
		height: 100%;
		width: 3px;
		position: absolute;
		@media only screen and (max-width: 800px) {
			justify-self: flex-start;
			left: 5px;
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
	&__text {
		font-size: 18px;
		max-width: 60ch;
		line-height: 27px;
		text-align: center;
		letter-spacing: 0.2px;
	}
}
</style>
