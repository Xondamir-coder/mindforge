<template>
	<section class="directions section-padding">
		<h1 class="directions__title">
			Мы предлагаем готовые полноценные курсы на основе данных направлений:
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
import directionsImg1 from '@/assets/images/directions-1.png';
import directionsImg2 from '@/assets/images/directions-2.png';
import directionsImg3 from '@/assets/images/directions-3.jpg';
import directionsImg4 from '@/assets/images/directions-4.jpg';
import directionsImg5 from '@/assets/images/directions-5.jpg';
import directionsImg6 from '@/assets/images/directions-6.jpg';
import directionsImg7 from '@/assets/images/directions-7.jpg';
import directionsImg8 from '@/assets/images/directions-8.jpg';
import directionsImg10 from '@/assets/images/directions-10.jpg';
import directionsImg11 from '@/assets/images/directions-11.jpg';

const contents = [
	{
		title: 'ACCA',
		img: directionsImg1,
		data: [
			'Корпоративное управление',
			'Управление рисками',
			'Этика и корпоративная культура',
			'Управление эффективностью',
			'Финансовый менеджмент',
			'Финансовая отчетность',
			'Управленческий учет'
		]
	},
	{
		title: 'CIMA',
		img: directionsImg2,
		data: [
			'E1 - Организационный менеджмент',
			'E2 - Управление проектами и управляющие взаимоотношения',
			'E3 - Стратегическое управление',
			'F3 - Финансовая стратегия',
			'P1 - Управление эффективностью операций',
			'P2 - Управление эффективностью бизнеса',
			'P3 - Управление рисками'
		]
	},
	{
		title: 'Бизнес менеджмент',
		img: directionsImg3,
		data: [
			'Бизнес менеджмент',
			'Бизнес процессы',
			'Бизнес этика',
			'Бизнес коммуникации',
			'Финансы',
			'Аналитика',
			'Управление персоналом'
		]
	},
	{
		title: 'Инженерия',
		img: directionsImg4,
		data: [
			'Гидромеханика',
			'Пневматика',
			'Электроника',
			'Робототехника',
			'Строительная инженерия',
			'Сопромат'
		]
	},
	{
		title: 'Технологии',
		img: directionsImg5,
		data: [
			'Языки программирования',
			'WEB разработка',
			'Дизайн',
			'Тестирования',
			'Data Science',
			'Машинное обучение'
		]
	},
	{
		title: 'Наука',
		img: directionsImg6,
		data: ['Высшая математика', 'Статистика', 'Эконометрика', 'Физика-2', 'Химия']
	},
	{
		title: 'Управление проектами',
		img: directionsImg7,
		data: [
			'Проектное управление (PMBOK, PRINCE2, AGILE)',
			'SCRUM',
			'KANBAN',
			'LEAN',
			'Управление изменениями'
		]
	},
	{
		title: 'Софт и инструменты',
		img: directionsImg8,
		data: [
			'Пакет AutoDesk',
			'Пакет Adobe',
			'Пакет MS OFFICE',
			'DINAMO BIM',
			'SolidWorks',
			'MatLab'
		]
	},
	{
		title: 'Психология',
		img: directionsImg10,
		data: ['Социальная психология', 'Бизнес психология', 'Теория игр', 'Когнитивная психология']
	},
	{
		title: 'Языки',
		img: directionsImg11,
		data: [
			'Английский',
			'Китайский',
			'Русский',
			'Немецкий',
			'Французский',
			'Итальянский',
			'Испанский',
			'Японский',
			'Корейский'
		]
	}
];
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
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		list-style: none;
		column-gap: 3rem;
		row-gap: 6rem;
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
		opacity: 0;
		transform: translateY(4rem);
		transition: opacity 400ms, transform 400ms;
	}
	&__item {
		display: grid;
		grid-template-rows: 300px max-content;
		gap: 30px;
		transform: perspective(800px) rotateX(40deg) translateZ(100px);
		transition: transform 1s, opacity 1s;
		opacity: 0;
		@for $i from 1 through 10 {
			&:nth-child(#{$i}) {
				transition-delay: $i * 0.3s;
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
			text-align: center;
			font-size: 18px;
		}
	}
}
</style>
