<template>
	<section class="cta section-padding">
		<div class="cta__links">
			<div class="cta__link">
				<IconMail />
				<p>Ищете помощь? <a href="#">Напишите нам сегодня</a></p>
			</div>
			<div class="cta__link">
				<IconLike class="cta__icon" />
				<p>Оставайтесь на связи. <a href="#">Подпишитесь на нас в Facebook</a></p>
			</div>
		</div>
	</section>
</template>

<script setup>
import IconLike from './icons/IconLike.vue';
import IconMail from './icons/IconMail.vue';
</script>

<style lang="scss" scoped>
.cta {
	position: relative;
	&__link {
		display: flex;
		align-items: center;
		gap: 1rem;
		color: var(--dark-gray);
		font-weight: 500;
	}
	&__links {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		column-gap: 10rem;
		row-gap: 4rem;
		font-size: 20px;
		margin-bottom: 8rem;
		a {
			font-weight: bold;
			color: inherit;
		}
	}
}
</style>
