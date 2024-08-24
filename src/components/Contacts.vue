<template>
	<section class="contacts section-padding">
		<h1 class="contacts__title">{{ $t('contacts-title') }}</h1>
		<form class="form" @submit.prevent="submitForm">
			<div class="form__container" v-for="content in contents" :key="content.name">
				<h2 class="form__label">{{ content.title }}</h2>
				<div class="form__box">
					<input
						:type="
							content.name == 'message' ||
							content.name == 'subject' ||
							content.name == 'name'
								? 'text'
								: content.name
						"
						class="form__input"
						:name="content.name"
						:placeholder="content.desc"
						:required="content.isRequired"
						v-model="data[content.name]" />
					<component class="form__icon" :is="content.icon" />
					<IconError class="form__icon-validity form__icon-invalid" />
					<IconValid class="form__icon-validity form__icon-valid" />
				</div>
			</div>
			<button type="submit"></button>
		</form>
		<div class="contacts__footer">
			<p>
				{{ $t('contacts-classified') }}
			</p>
			<Button
				@click="submitForm"
				:label="$t('send')"
				:icon="IconSend"
				class="contacts__button" />
		</div>
	</section>
</template>

<script setup>
import IconCall from './icons/IconCall.vue';
import IconMail from './icons/IconMail.vue';
import IconSmile from './icons/IconSmile.vue';
import IconTopic from './icons/IconTopic.vue';
import IconMessage from './icons/IconMessage.vue';
import { computed, ref } from 'vue';
import IconError from './icons/IconError.vue';
import IconValid from './icons/IconValid.vue';
import IconSend from './icons/IconSend.vue';
import Button from './Button.vue';
import { i18n } from '@/locales';

const contents = computed(() => [
	{
		name: 'name',
		icon: IconSmile,
		isRequired: true,
		desc: i18n.global.t('contacts-desc-1'),
		title: i18n.global.t('contacts-title-1')
	},
	{
		name: 'email',
		icon: IconMail,
		isRequired: true,
		desc: i18n.global.t('contacts-desc-2'),
		title: i18n.global.t('contacts-title-2')
	},
	{
		name: 'tel',
		icon: IconCall,
		isRequired: true,
		desc: i18n.global.t('contacts-desc-3'),
		title: i18n.global.t('contacts-title-3')
	},
	{
		name: 'subject',
		icon: IconTopic,
		isRequired: false,
		desc: i18n.global.t('contacts-desc-4'),
		title: i18n.global.t('contacts-title-4')
	},
	{
		name: 'message',
		icon: IconMessage,
		isRequired: false,
		desc: i18n.global.t('contacts-desc-5'),
		title: i18n.global.t('contacts-title-5')
	}
]);

const data = ref({
	name: '',
	email: '',
	tel: '',
	subject: '',
	message: ''
});

const submitForm = () => {
	Object.keys(data.value).forEach(key => {
		data.value[key] = data.value[key].trim();
	});
	console.log(data.value);
	if (!data.value.name || !data.value.email || !data.value.tel) return;
	console.log(data.value);
};
</script>

<style lang="scss" scoped>
.form {
	display: grid;
	grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
	width: 100%;
	max-width: 900px;
	gap: 4rem;
	button {
		display: none;
	}
	@media only screen and (max-width: 500px) {
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
	}
	&__container {
		display: flex;
		flex-direction: column;
		gap: 1rem;
		opacity: 0;
		transform: translateY(50px);
		transition: opacity 400ms, transform 400ms;

		&:nth-of-type(2) {
			transition-delay: 300ms;
		}

		&:nth-of-type(3) {
			transition-delay: 500ms;
		}

		&:nth-of-type(4) {
			transition-delay: 700ms;
		}
		&:last-of-type {
			grid-column: span 2;
			transition-delay: 900ms;
			@media only screen and (max-width: 800px) {
				grid-column: initial;
			}
			.form__icon-validity {
				display: none;
			}
			.form__box {
				border-bottom: none;
			}
		}
	}
	&__box {
		position: relative;
		display: flex;
		align-items: center;
		gap: 15px;
		border-bottom: 1px solid var(--extra-medium-gray);
		transition: border-color 300ms;
		&:has(.form__input:user-invalid) {
			border-color: #dc3545;
		}
	}
	&__icon {
		width: 2rem;
		height: 2rem;
		&-validity {
			position: absolute;
			right: 3rem;
			top: 50%;
			transform: translateY(-50%);
			width: 2rem;
			height: 2rem;
			opacity: 0;
			transition: opacity 300ms;
		}
	}
	&__input {
		flex: 1;
		border: none;
		background-color: transparent;
		font: inherit;
		color: var(--medium-gray);
		font-size: 16px;
		padding: 2.2rem 0;
		outline: none;
		&:user-valid ~ .form__icon-valid {
			opacity: 1;
		}
		&:user-invalid ~ .form__icon-invalid {
			opacity: 1;
		}
	}
	&__label {
		font-size: 14px;
		font-weight: 600;
	}
}
.contacts {
	display: flex;
	flex-direction: column;
	align-items: center;
	gap: 5rem;
	&.active &__title {
		transform: translateY(0);
		opacity: 1;
	}
	&.active .form__container {
		transform: translateY(0);
		opacity: 1;
	}
	&__footer {
		display: flex;
		row-gap: 3rem;
		flex-wrap: wrap;
		align-items: center;
		padding: 3rem 0;
		width: 100%;
		max-width: 900px;
		line-height: 1.5;
		margin-top: 5rem;
		border-top: 1px solid var(--extra-medium-gray);
		justify-content: space-between;
		p {
			max-width: 50ch;
			font-size: 15px;
			color: rgb(130, 140, 138);
		}
	}
	&__title {
		font-size: 5.5rem;
		font-weight: 600;
		font-family: var(--font-alt);
		letter-spacing: -3px;
		transform: translateY(30px);
		opacity: 0;
		transition: transform 400ms, opacity 400ms;
	}
	&__button {
		background-color: var(--dark-gray);
		color: #fff;
	}
}
</style>
