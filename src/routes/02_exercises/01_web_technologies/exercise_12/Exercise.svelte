<script>
	let clicked = false;
</script>

<div>
	<button class="btn btn-primary" on:click={() => (clicked = 1-clicked)}>
		click here
	</button>
	<!--  -->
</div>

{#if clicked}
You have clicked the button!
{:else}
You have to click the button!
{/if}