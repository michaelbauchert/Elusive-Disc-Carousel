<script>
	import ElusiveCarousel from './ElusiveCarousel.svelte';
	
	let slides = [
		{
			image: "https://picsum.photos/id/237/620/640",
			altText: "",
			text: "Slide 1",
			heading: "Cute Dog",
			buttonText: "Blurry Background"
		},
		{
			image: "https://picsum.photos/id/236/620/640",
			altText: "",
			text: "on rocks",
			heading: "Houses",
			buttonText: "dull colors"
		},
		{
			image: "https://picsum.photos/id/238/620/640",
			altText: "",
			text: "Lots of windows",
			heading: "Tall buildings",
			buttonText: "Duller colors"
		},
		{
			image: "https://picsum.photos/id/239/620/640",
			altText: "Slide 4",
			text: "seeds get everywhere",
			heading: "Dandelion",
			buttonText: "woosh"
		}
	];
</script>

<h1>Elusive Disc Carousel</h1>

<main>
	<ElusiveCarousel duration="4000" slides={slides} />
</main>

<p>This carousel was created from scratch using <a href="https://svelte.dev">Svelte</a> in preparation of the launch of Elusive Disc's new, eCommerce website. It is fully responsive, integrages seamlessly with Bigcommerce, and looks great.</p>

<style>
	main {
		display: flex;
		justify-content: center;
	}
	
	h1, p {
		text-align: center;
	}
</style>
