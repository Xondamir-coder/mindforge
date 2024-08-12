<template>
	<button class="button">
		<icon />
		<span class="button-span">{{ label }}</span>
	</button>
</template>

<script setup>
import IconLike from './icons/IconLike.vue';

const props = defineProps({
	label: String,
	icon: {
		default: IconLike,
		type: Object
	}
});
</script>

<style lang="scss" scoped>
.button {
	display: flex;
	align-items: center;
	justify-content: center;
	gap: 1rem;
	background-color: var(--base-color);
	color: var(--dark-gray);
	font-size: 1.7rem;
	font-weight: 500;
	padding: 2rem 3rem;
	border-radius: 100px;
	font-weight: 600;
	cursor: pointer;
	border: none;
	overflow: hidden;
	box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);

	&:hover {
		& .button-span {
			transform: translateY(-200%);
			&::after {
				opacity: 1;
			}
		}
	}
	&-span {
		transition: transform 300ms, opacity 300ms;
		position: relative;

		&::after {
			content: 'Get started';
			font: inherit;
			position: absolute;
			top: 0;
			left: 0;
			transform: translateY(200%);
			opacity: 0;
			transition: transform 300ms, opacity 300ms;
		}
	}
}
</style>
