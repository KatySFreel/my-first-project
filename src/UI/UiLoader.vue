<template>
	<div class="loader">
		<img
			src="../../public/loading.gif"
			alt="Загрузка"
			class="loader__img"
		>
	</div>
</template>

<style>
	.loader {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.loader__img {
		width: 200px;
		height: 180px;
	}
</style>
