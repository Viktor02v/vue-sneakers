<script setup>
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'
</script>

<template>
	<!-- <Drawer /> -->

	<div class="w-4/5 m-auto bg-white rounded-xl	shadow-xl mt-14">
		<Header />

		<div class="p-10">
			<div class="flex justify-between">
				<h2 class="text-3xl font-bold mb-8">Shoes list</h2>
				<div>
					<input placeholder="Search" class="border rounded-md pl-10 py-2 pr-4 outline-none focus:border-gray-500"
						type="text">
				</div>
			</div>

			<CardList />
		</div>

	</div>
</template>
<style></style>