<script setup>
import Card from './Card.vue'

const onCLickAdd  = () => {
	alert(111);
}
</script>

<template>
	<div class="grid grid-cols-4 gap-5">
		<Card title="Man's Shoes Nike Blazer Mid Suede" :price="5000" imageUrl="/sneakers/sneakers-1.jpg"
			:is-added="false" :is-favorite="false" :onClickAdd="onCLickAdd" />
	</div>
</template>