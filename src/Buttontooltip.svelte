<script>	
	export let tooltip = false
</script>

<button data-tooltip={tooltip}>
	<slot></slot>
</button>

<style>
	button {
		margin-left:50px;
        margin-top: 200px;
	}
</style>