<script setup>
import { onMounted, reactive, ref, watch } from 'vue';
import axios from 'axios';

import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'
import CssSyntaxError from 'postcss/lib/css-syntax-error';

const items = ref([])

const filters = reactive({
	sortBy: 'title',
	searchQuery: '',
})

const onChange = (e) => {
	filters.sortBy = (e.target.value)
}

const onChangeQuery = (e) => {
	filters.searchQuery = (e.target.value)
}

// Get the Data For Favorites(for Tabs)
const fetchFavorites = async () => {
	try {
		const { data: favorites } = await axios.get(`https://ed0472d2c8c161f9.mokky.dev/favorites`)
		items.value = items.value.map(item => {
			const favorite = favorites.find(favorite => favorite.productId === item.id);

			if (!favorite) {
				return item;
			}

			return {
				...item,
				isFavorite: true,
				favoriteId: favorite.id,
			}
		});
	} catch (error) {
		console.log(error)
	}
}

const addToFavorites = async (item) => {
	try {
		
		if (!item.isFavorite) {
			const obj = {
				productId: item.id,
			}
			item.isFavorite = true
			const { data } = await axios.post(`https://ed0472d2c8c161f9.mokky.dev/favorites`, obj);
			item.favoriteId = data.id;
		} else {
			item.isFavorite = false
			await axios.delete(`https://ed0472d2c8c161f9.mokky.dev/favorites/${item.favoriteId}`);
			item.favoriteId = null;

		}
	} catch (error) {
		console.log(error)
	}
}
// Get The Data For Items And Filters
const fetchItems = async () => {
	try {
		const params = {
			sortBy: filters.sortBy,
		}

		if (filters.searchQuery) {
			params.title = `*${filters.searchQuery}*`
		}
		const { data } = await axios.get(
			`https://ed0472d2c8c161f9.mokky.dev/items`,
			{
				params
			})
		items.value = data.map((obj) => ({
			...obj,
			isFavorite: false,
			favoriteId: null,
			isAdded: false
		}));
	} catch (error) {
		console.log(error)
	}
}

onMounted(async () => {
	await fetchItems();
	await fetchFavorites()
});
watch(filters, fetchItems);

</script>

<template>
	<!-- <Drawer /> -->

	<div class="w-4/5 m-auto bg-white rounded-xl	shadow-xl mt-14">
		<Header />

		<div class="p-10">

			<div class="flex items-center justify-between">

				<h2 class="text-3xl font-bold mb-8 ">Shoes list</h2>
				<div class="flex gap-4">
					<select @change="onChange" class="py-2 px-3 border rounded-md outline-none" name="" id="">
						<option value="title">By name</option>
						<option value="price">By price (Cheap)</option>
						<option value="-price">By price (Expensive)</option>
					</select>

					<div class="relative">
						<img class="absolute top-2.5 left-4" src="/search.svg">
						<input @input="onChangeQuery" placeholder="Search"
							class=" border rounded-md pl-11 py-1.5 pr-4 outline-none focus:border-gray-500" type="text">
					</div>
				</div>
			</div>

			<div class="mt-10">
				<CardList :items="items" @addToFavorites="addToFavorites" />
			</div>
		</div>

	</div>
</template>
<style></style>