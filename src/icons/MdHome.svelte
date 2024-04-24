<script>
	export let selected = false;
</script>

{#if selected}
	<svg
		xmlns="http://www.w3.org/2000/svg"
		viewBox="0 -960 960 960"
		stroke="currentColor"
		fill="currentColor"
		height="1em"
		width="1em"
		{...$$restProps}
		><path d="M160-120v-480l320-240 320 240v480H560v-280H400v280H160Z" /></svg
	>
{:else}
	<svg
		xmlns="http://www.w3.org/2000/svg"
		viewBox="0 -960 960 960"
		height="1em"
		width="1em"
		{...$$restProps}
		><path
			d="M240-200h120v-240h240v240h120v-360L480-740 240-560v360Zm-80 80v-480l320-240 320 240v480H520v-240h-80v240H160Zm320-350Z"
		/></svg
	>
{/if}
