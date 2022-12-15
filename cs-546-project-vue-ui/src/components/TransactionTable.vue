<template>
	<div class="px-4 sm:px-6 lg:px-8">
		<div class="sm:flex sm:items-center">
			<div class="sm:flex-auto mt-6">
				<h1 class="text-xl font-semibold text-gray-900">{{ props.orders.name }}</h1>
				<p class="mt-2 text-sm text-gray-700">{{ props.orders.description }}</p>
			</div>
			<div class="mt-4 sm:mt-0 sm:ml-16 sm:flex-none">
				<button type="button" class="inline-flex items-center justify-center rounded-md borders borders-transparent bg-indigo-600 px-4 py-2 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 sm:w-auto">
					Export
				</button>
			</div>
		</div>
		<div class="mt-8 flex flex-col">
			<div class="-my-2 -mx-4 overflow-x-auto sm:-mx-6 lg:-mx-8">
				<div class="inline-block min-w-full py-2 align-middle md:px-6 lg:px-8">
					<div class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 md:rounded-lg">
						<table class="min-w-full divide-y divide-gray-300">
							<thead class="bg-gray-50">
								<tr>
									<th scope="col" class="whitespace-nowrap py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6">Transaction ID</th>
									<th scope="col" class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900">Company</th>
									<th scope="col" class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900">Share</th>
									<th scope="col" class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900">Commision</th>
									<th scope="col" class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900">Price</th>
									<th scope="col" class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900">Quantity</th>
									<th scope="col" class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900">Net amount</th>
									<th scope="col" v-if="orders.name === 'Fulfilled Orders'" class="relative whitespace-nowrap py-3.5 pl-3 pr-4 sm:pr-6">
										<span class="sr-only">Edit</span>
									</th>
								</tr>
							</thead>
							<tbody class="divide-y divide-gray-200 bg-white">
								<tr v-for="transaction in props.orders.data" :key="transaction.id">
									<td class="whitespace-nowrap py-2 pl-4 pr-3 text-sm text-gray-500 sm:pl-6">{{ transaction.id }}</td>
									<td class="whitespace-nowrap px-2 py-2 text-sm font-medium text-gray-900">{{ transaction.company }}</td>
									<td class="whitespace-nowrap px-2 py-2 text-sm text-gray-900">{{ transaction.share }}</td>
									<td class="whitespace-nowrap px-2 py-2 text-sm text-gray-500">{{ transaction.commission }}</td>
									<td class="whitespace-nowrap px-2 py-2 text-sm text-gray-500">{{ transaction.price }}</td>
									<td class="whitespace-nowrap px-2 py-2 text-sm text-gray-500">{{ transaction.quantity }}</td>
									<td class="whitespace-nowrap px-2 py-2 text-sm text-gray-500">{{ transaction.netAmount }}</td>
									<td v-if="orders.name === 'Fulfilled Orders'" class="relative whitespace-nowrap py-2 pl-3 pr-4 text-right text-sm font-medium sm:pr-6">
										<button
											type="button"
											@click="open = true"
											class="inline-flex items-center rounded-md border border-transparent bg-indigo-600 px-2 py-2 text-sm font-medium leading-4 text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
										>
											Rate
											<StarIcon class="ml-2 -mr-0.5 h-4 w-4" aria-hidden="true" />
										</button>
									</td>
								</tr>
							</tbody>
						</table>
					</div>
				</div>
			</div>
		</div>
	</div>
	<ProductModal :open="open" @close="open = false" />
</template>

<script setup>
import { ref } from "vue";
import { StarIcon } from "@heroicons/vue/24/solid";
import ProductModal from "./ProductModal.vue";

let open = ref(false);
const props = defineProps(["orders"]);
</script>