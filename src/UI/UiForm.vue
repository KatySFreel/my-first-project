<template>
	<div class="ui-form">
		<h2>
			{{ type === 'addCard' ? 'Форма создания' : 'Форма редактирования' }}
		</h2>

		<p
			v-if="type === 'editCard'"
			class="ui-form__text"
		>
			Для редактирования кликните по карточке, которую хотите изменить
		</p>

		<form
			@submit.prevent="sendCard"
			class="ui-form__form"
		>
			<label>
				Название

				<input
					v-if="type === 'addCard'"
					type="text"
					v-model="newCard.title"
				/>

				<input
					v-else
					type="text"
					:value="card.title"
					@input="setTitle"/>
			</label>

			<label>
				Описание

				<input
					v-if="type === 'addCard'"
					type="text"
					v-model="newCard.description"/>

				<input
					v-else
					type="text"
					:value="card.description"
					@input="setDescription"/>
			</label>

			<button
				type="submit"
				class="ui-form__btn"
			>
				{{ type === 'addCard' ? 'Сохранить' : 'Добавить' }}
			</button>
		</form>
	</div>
</template>

<script setup>
import {ref} from "vue";

const props = defineProps({
	card: {
		type: Object,
		required: false
	},
	type: {
		type: String,
		required: true
	}
})

const emit = defineEmits([
	'set-card',
	'save-card'
])

const newCard = ref({
	id: 0,
	title: '',
	description: '',
	completed: false
})

const setTitle = (event) => {
	const data = Object.assign({}, props.card)
	data.title = event.target.value
	emit('set-card', data)
	console.log('setTitle')
}

const setDescription = (event) => {
	const data = Object.assign({}, props.card)
	data.description = event.target.value
	emit('set-card', data)
	console.log('setDescription')
}

const sendCard = () => {
	if (props.type === 'addCard') {
		addCard()
	} else {
		editCard()
	}
}

const addCard = () => {
	emit('set-card', newCard.value)
	console.log('addCard')
}

const editCard = () => {
	emit('save-card')
	console.log('editCard')
}
</script>

<style>
.ui-form__text {
	margin-bottom: 20px;
}

.ui-form__form {
	display: flex;
	flex-direction: column;
}

.ui-form__btn {
	width: fit-content;
}
</style>
