<template>
	<div class="lg:w-1/5 border-r px-2 lg:px-6 py-2 flex flex-col justify-between">
		<div>
			<slot name="twitter-logo"></slot>
			<div>
				<slot name="twitter-tabs"></slot>
			</div> <!-- NAIGATION LINKS -->
			<slot name="twitter-button"></slot>
		</div>
		<div class="w-full relative">
			<slot name="twitter-avatar"></slot>
		</div>
	</div> <!-- END SIDE BAR -->
</template>