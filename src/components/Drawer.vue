<script setup>
import DrawerHead from './DrawerHead.vue'
import BasketItemList from './BasketItemList.vue'
import InfoBlock from './InfoBlock.vue'
const emit = defineEmits(['createOrder'])

defineProps({
	totalPrice: Number,
	vatPrice: Number,
	buttonDisabled: Boolean,
})

</script>
<template>
	<div class="fixed top-0 left-0 w-full h-full bg-black/50 z-10 ">
		<div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
			<DrawerHead />

			<div v-if="!totalPrice" class="flex h-full items-center">
				<InfoBlock title="Your cart is empty." description="Add some items in here" image-url="/package-icon.png" />
			</div>

			<div v-else>
				<BasketItemList />
				<div v-if="totalPrice" class="flex flex-col gap-4 mt-7">
					<div class="flex gap-2">
						<span>
							In Total:
						</span>
						<div class="flex-1 border-b border-dashed"></div>
						<b>{{ totalPrice }} UAN</b>
					</div>

					<div class="flex gap-2">
						<span>
							Tax 5%:
						</span>
						<div class="flex-1 border-b border-dashed"></div>
						<b>{{ vatPrice }} UAN</b>
					</div>

					<button @click="emit('createOrder')" :disabled="buttonDisabled"
						class="mt-4 transition disabled:bg-slate-300 bg-lime-500 w-full rounded-xl py-3 text-white hover:bg-lime-600 active:bg-lime-700 cursor-pointer">Make
						an order </button>
				</div>
			</div>
		</div>
	</div>
</template>