<script setup>
import Card from './Card.vue'

defineProps({
	items: Array,
})

const emit = defineEmits(['addToFavorites'])

const onClickAdd = () => {
	alert('Added')
}



</script>

<template>
	<div class="grid grid-cols-4 gap-5">

		<Card v-for="item in items" :key="item.id" :id="item.id" :title="item.title" :price="item.price"
			:imageUrl="item.imageUrl" :onClickAdd="onClickAdd" :onClickFavorites="()=>emit('addToFavorites', item)"
			:isFavorite="item.isFavorite" />

	</div>
</template>