<template>
	<div class="w-1/2 h-full overflow-y-scroll">
		<div class="px-5 py-3 border-b border-gray-300 flex items-center justify-between">
			<slot name="home-title"></slot>
		</div>
		<div class="px-5 py-3 border-b-8 border-gray-300 flex">
			<slot name="tweet-field"></slot>
		</div>
		<div class="flex flex-col-reverse">
			<slot name="tweet-user-fresh-post"></slot>
		</div>
		<slot name="tweet-posts"></slot>
	</div>
</template>