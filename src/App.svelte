<script>

	let products = [{
		id: 1,
		name: 'HP Pavilion Notebook',
		description: 'HP Laptop',
		category: 'laptop'
	},
	{
		id: 2,
		name: 'Mouse Razer',
		description: 'Gaming Mouse',
		category: 'peripherials'
	}
	]

	let product = {
		id: "", 
		name: "", 
		description: "", 
		category:"", 
		imageURL:""
	};

	const cleanProduct = () => {
		product = {
			id: "",
			name: "",
			description: "",
			category: "",
			imageURL: ""
		}
	}

	//https://www.pcgamesn.com/wp-content/uploads/2018/09/Best-gaming-keyboard-runner-up-Ducky-One2-Horizon.jpg

	const onSubmitHandler = e => {
		e.preventDefault();
		//console.log(product)
		const newProduct = {
			id: products.length,
			name: product.name,
			description: product.description,
			category: product.category,
			imageURL: product.imageURL
		}

		products = products.concat(newProduct)
		cleanProduct();
	}

	const deleteProduct = (id) =>{
		console.log(products);
		products = products.filter(product => product.id !== id);
	}

</script>

<main>
	<form on:submit={onSubmitHandler}>
		<input bind:value={product.name} type="text" placeholder="Product Name" id="product-name">
		
		<textarea 
			bind:value={product.description}
			id="product-description" 
			rows="3" 
			placeholder="Product Description" />

		<input
			bind:value={product.imageURL}
			type="url" 
			id="product-image-url" 
			placeholder="" />
			
		<select id="category" bind:value={product.category}>
			<option value="laptops">Laptops</option>
			<option value="peripherials">Peripherials</option>
			<option value="Servers">Servers</option>
		</select>

		<button>
			Save Product
		</button>
	</form>

	<div class="">
		{#each products as product}
			<div style="border:solid 1px black">
				{#if !product.imageURL}
					<img class="image" alt="" src="https://www.pinclipart.com/picdir/big/189-1894636_mayonnaise-clip-art.png" />
				{:else}
					<img class="image" alt="" src="{product.imageURL}" />
				{/if}
				
				<h1>{product.name}</h1>
				<h5>{product.description}</h5>
				<h4>{product.category}</h4>
			</div>
			<div>
				<button on:click={deleteProduct(product.id)}> 
					Delete
				</button>

				<button>
					Edit
				</button>
			</div>
		{/each}
	</div>
</main>

<style>
	.image{
		width:150px;
	}
</style>