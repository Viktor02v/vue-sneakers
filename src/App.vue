<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';

import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'

const items = ref([]);

onMounted(async () => {
	try {
		const { data } = await axios.get('https://ed0472d2c8c161f9.mokky.dev/items')
		items.value = data;
	} catch (error) {
		console.log(error)
	}
})
</script>

<template>
	<!-- <Drawer /> -->

	<div class="w-4/5 m-auto bg-white rounded-xl	shadow-xl mt-14">
		<Header />

		<div class="p-10">

			<div class="flex items-center justify-between">

				<h2 class="text-3xl font-bold mb-8 ">Shoes list</h2>
				<div class="flex gap-4">
					<select class="py-2 px-3 border rounded-md outline-none" name="" id="">
						<option value="">By name</option>
						<option value="">By price (Cheap)</option>
						<option value="">By price (Expensive)</option>
					</select>

					<div class="relative">
						<img class="absolute top-2.5 left-4" src="/search.svg">
						<input placeholder="Search"
							class=" border rounded-md pl-11 py-1.5 pr-4 outline-none focus:border-gray-500" type="text">
					</div>
				</div>
			</div>

			<div class="mt-10">
				<CardList :items="items" />
			</div>
		</div>

	</div>
</template>
<style></style>