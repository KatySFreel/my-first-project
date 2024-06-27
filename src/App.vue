<template>
	<main class="start-screen">
		<div class="container">
			<div
				v-if="!cardsIsLoading"
				class="start-screen__wrapper"
			>
				<div class="start-screen__btns">
					<button
						type="button"
						class="start-screen__btn btn"
						@click="openForm('addCard')"
					>
						Создать новое желание
					</button>

					<button
						type="button"
						class="start-screen__btn btn"
						@click="openForm('editCard')"
					>
						Редактировать желание
					</button>
				</div>

				<UiForm
					v-if="isShowEditCardForm"
					type="editCard"
					:card="cardFormEdit"
					@set-card="updateCard"
					@save-card="saveCard"
				/>

				<UiForm
					v-if="isShowAddCardForm"
					type="addCard"
					@set-card="addCard"
				/>

				<WishList
					:cards="cards"
					@click-by-card="openCardFormEdit"
				/>
			</div>

			<UiLoader v-else/>
		</div>
	</main>
</template>

<script setup>
import {ref} from 'vue'

import UiForm from "./UI/UiForm.vue";
import UiLoader from "@/UI/UiLoader.vue";
import WishList from "./components/WishList.vue";

const cards = ref([])
const cardsIsLoading = ref(false)

const loadCards = () => {
	cardsIsLoading.value = true

	setTimeout(() => {
		cards.value =  [
			{
				id: 1,
				title: "Ноутбук",
				description: "Я хочу получить в подарок новый ноутбук",
				completed: false
			},
			{
				id: 2,
				title: "Наушники",
				description: "Я хочу получить в подарок наушники для ноутбука",
				completed: true
			},
			{
				id: 3,
				title: "Мышка",
				description: "Я хочу получить в подарок мышку для ноутбука",
				completed: false
			}
		]

		cardsIsLoading.value = false
	}, 2000)
}

loadCards()

const isShowAddCardForm = ref(false)
const isShowEditCardForm = ref(false)

const cardFormEdit = ref({
	id: 0,
	title: '',
	description: '',
	completed: false
})

const openForm = (form) => {
	if (form === 'addCard') {
		isShowAddCardForm.value = !isShowAddCardForm.value
		isShowEditCardForm.value = false
	} else {
		isShowEditCardForm.value = !isShowEditCardForm.value
		isShowAddCardForm.value = false
	}
}

const addCard = (card) => {
	cards.value.push(card);
	isShowAddCardForm.value = false;
	console.log(addCard.name)
}

const saveCard = () => {
	const newCard = Object.assign({}, cardFormEdit.value)
	cards.value = cards.value.map(el => el.id === newCard.id ? newCard : el)
	isShowEditCardForm.value = false;
	console.log(saveCard.name)
}

const openCardFormEdit = (card) => {
	cardFormEdit.value = Object.assign({}, card)
	console.log(openCardFormEdit.name)
}

const updateCard = (card) => {
	cardFormEdit.value = card
	console.log(updateCard.name)
}
</script>

<style>
@import './assets/global.css';

.start-screen__btns {
	display: flex;
	column-gap: 12px;
}
</style>