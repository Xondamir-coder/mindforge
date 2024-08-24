<template>
	<header class="header" ref="headerRef">
		<a href="#"><Logo class="header__logo" /></a>
		<div class="header__right">
			<ul class="header__languages">
				<li
					class="header__language"
					v-for="{ label, lang } in [
						{ label: 'O\'ZB', lang: 'uz' },
						{ label: 'РУС', lang: 'ru' },
						{ label: 'ENG', lang: 'en' }
					]">
					<button @click="selectLang(lang)">
						{{ label }}
					</button>
				</li>
			</ul>
		</div>
	</header>
</template>

<script setup>
import { changeLang } from '@/locales';
import Logo from './icons/Logo.vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { onMounted, ref } from 'vue';
gsap.registerPlugin(ScrollTrigger);
const headerRef = ref();

const selectLang = lang => changeLang(lang);

onMounted(() => {
	gsap.timeline({
		scrollTrigger: {
			trigger: headerRef.value,
			start: '+=200 top',
			endTrigger: document.body,
			toggleActions: 'play none none reverse'
		}
	})
		.to(headerRef.value, {
			y: '-100%'
		})
		.to(headerRef.value, {
			backgroundColor: '#fff',
			color: 'var(--dark-gray)',
			boxShadow: '0 0px 20px 4px rgba(0, 0, 0, 0.25)',
			y: 0,
			duration: 0.5
		});
});
</script>

<style lang="scss" scoped>
.header {
	width: 100%;
	display: flex;
	justify-content: space-between;
	position: fixed;
	z-index: 100;
	top: 0;
	padding: 2rem max(2rem, 5vw);
	font-family: var(--font-alt);
	// background-color: #fff;
	color: #fff;
	align-items: center;
	&__languages {
		list-style-type: none;
		display: flex;
		align-items: center;
	}
	&__language {
		padding: 0 2rem;
		&:not(:last-child) {
			border-right: 1px solid currentColor;
		}
		&:hover button {
			color: var(--base-color);
		}
		button {
			background-color: transparent;
			border: none;
			color: inherit;
			transition: color 300ms;
		}
	}
	&__right {
		display: flex;
		flex-wrap: wrap;
		gap: 2rem;
	}
	a {
		color: inherit;
	}
	&__logo {
		width: 15.7rem;
		height: 3.9rem;
		transition: color 300ms;
		&:hover {
			color: var(--base-color);
		}
	}
}
</style>
