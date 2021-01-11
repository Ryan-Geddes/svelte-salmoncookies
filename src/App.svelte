
<script>
	import IndexContent from './components/index.svelte';
	import Header from './components/header.svelte';
	import Footer from './components/footer.svelte';
	import SalesContent from './components/sales.svelte';

	
	let component = IndexContent;
	let props;

</script>




<main>

	<Header />
	<button on:click={()=>component = SalesContent}>Sales</button>
	<button on:click={()=>component = IndexContent}>Home</button>
	
	<svelte:component this={component} {...props}/>
	<Footer />
	
	
</main>


<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		background-color: rgb(231, 227, 223);
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>