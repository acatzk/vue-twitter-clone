<template>
	<div class="hidden md:block w-1/3 h-full border-l py-2 px-6 overflow-y-scroll relative">
		<slot name="twitter-search"></slot>
		
		<div class="w-full rounded-lg bg-gray-400 mt-3">
			<div class="flex items-center justify-between p-3">
				<slot name="trending-title"></slot>
			</div>
			<slot name="trending-list"></slot>
		</div>

		<div class="w-full rounded-lg bg-gray-400 my-4">
			<div class="p-3">
				<slot name="user-title"></slot>
			</div>
			<slot name="user-list"></slot>
		</div>

	</div>
</template>