<template>
	<div id="modal-body">
		<div id="modal">
 			<h2>Новый клиент успешно создан!</h2>

 			<button @click="$emit('closeModal')">ok</button>
  		</div>
	</div>
</template>



<style lang="scss">

#modal-body{
	position: fixed;
	top: 0;
	left: 0;
	height: 0;
	right: 0;
	height: 100%;
	background: rgba(0,0,0,.5);
	display: flex;
	justify-content: center;
	align-items: center;
	#modal{
		width: 500px;
		height: 500px;
		background: #ccc;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
}

</style>