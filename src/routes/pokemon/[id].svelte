<script lang="ts" context="module">
	export async function load({ page }) {
		const id = page.params.id
		const url = `https://pokeapi.co/api/v2/pokemon/${id}`
		const res = await fetch(url)
		const pokemon = await res.json()
		return { props: { pokemon } }
	}
</script>

<script lang="ts">
	export let pokemon
	const imgArray = [
		pokemon.sprites.front_default,
		pokemon.sprites.back_default,
		pokemon.sprites.front_shiny,
		pokemon.sprites.back_shiny,
	]
	let counter = 0
	let img = imgArray[counter]
	function updateImage() {
		if (counter < imgArray.length - 1) {
			counter++
			img = imgArray[counter]
		} else {
			counter = 0
			img = imgArray[counter]
		}
	}
	const types = pokemon.types.map((t) => t.type.name)
</script>

<div class="flex flex-col items-center">
	<h1 class="text-4xl text-center my-8 uppercase">{pokemon.name}</h1>
	<p>
		Type: <strong>{types}</strong> | Height:
		<strong
			>{pokemon.height} | Weight:
			<strong>{pokemon.weight}</strong></strong
		>
	</p>
	<img class="w-36" src={img} alt="" />
	<button
		class="bg-green-200 p-2 shadow-lg hover:shadow-xl hover:scale-105 transition 3"
		on:click={updateImage}>next image</button
	>
</div>
