<script>
	import { blur, fade, fly } from 'svelte/transition';
	import { backIn, expoInOut } from 'svelte/easing';
	
	let index = 0;
	export let duration = 5000;
	let timer = setInterval(function(){ incIndex()}, duration);
	
	function stopTimer() {
		clearInterval(timer);
	}
	
	function resumeTimer() {
		timer = setInterval(function(){ incIndex()}, duration);
	}
							
	function incIndex() {
		index = (index < slides.length -1) ? index + 1 : 0;
	}
	
	export let slides = [];	
</script>

<section on:mouseenter={stopTimer} on:mouseleave={resumeTimer}>
	<button class="arrow" on:click={() => index = (index != 0) ? index - 1 : slides.length - 1}>
		<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 22">
			<path d="M15.41 7.41L14 6l-6 6 6 6 1.41-1.41L10.83 12z" fill="white"/>
			<path d="M0 0h24v24H0z" fill="none"/>
		</svg>
	</button>
	
	<div id="buttons">
		{#each slides as slide, i}
			<button class="dot" on:click={() => index = i} class:active="{index === i}">			
				<span>&bull;</span>
			</button>
		{/each}
	</div>
	
	
	<button class="arrow" on:click={incIndex}>
		<svg xmlns="http://www.w3.org/2000/svg"viewBox="0 0 24 20">
			<path d="M10 6L8.59 7.41 13.17 12l-4.58 4.59L10 18l6-6z" fill="white"/>
			<path d="M0 0h24v24H0z" fill="none"/>
		</svg>
	</button>	
	
	{#each slides as slide, i}
		{#if index == i}
			<a href={slide.url}>
				<div>					
					<p class="heading" 
						 out:fly="{{ x: -40, duration: 400, easing: backIn}}"						 								 
						 in:fly="{{ x: 40, duration: 600, delay: 300}}">{slide.heading}</p>
					<p class="text" 
						 in:fly="{{ x: -40, duration: 600, delay: 300}}"
						 out:fly="{{ x: 40, duration: 400, easing: backIn}}">{slide.text}</p>
					<p class="buttonText" 
						 transition:blur="{{amount: 5, duration: 800, easing: expoInOut}}">{slide.buttonText}</p>
				</div>
				<img src={slide.image} 
						 alt={slide.altText} 
						 title={slide.altText} 
						 transition:blur="{{amount: 5, duration: 800, easing: expoInOut}}">
			</a>
		{/if}
	{/each}
</section>


<style>
	/*Carousel Controls CSS*/
	svg {
		width: 7vw;
		filter: drop-shadow(var(--shadow));
	}	
	
	button, div {		
		align-self: flex-end;
		z-index: 2;		
		cursor: pointer;
	}
	
	button {
		opacity: 0;
		filter: brightness(1);
		transition: filter 0.2s, opacity 0.3s, backdrop-filter 0.1s;
	}
	
	button:hover:not(.active) {
		filter: brightness(0.6);
	}
	
	section:hover button {
		opacity: 1;
		overflow: hidden;
	}
	
	.arrow {		
		opacity: 0;
		align-self: center;
		background: none;
		border: none;
	}
	
	section {
		--width: calc(1108px / 3 * 2 - 10px);
		--shadow: 1px 2px 6px #111;
		width: var(--width);
		height: calc(var(--width) / 16 * 9);
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		background-color: black;
	}	
	
	span {
		text-shadow: var(--shadow);
	}
	
	.dot {
		background: none;
		border: none;
		color: #fff;
		font-size: calc(var(--width) / 14);
		padding: 0;		
	}
	
	.active {	
		mix-blend-mode: multiply;		
	}
	
	.active span {
		background-color: #565656;
		color: transparent;
		text-shadow: 2px 2px 3px rgba(255,255,255,0.2);
		-webkit-background-clip: text;
			 -moz-background-clip: text;
						background-clip: text;	
	}
	
	/*Slide CSS*/
	a div {		
		position: absolute;
		text-align: center;
		width: 100%;	
		height: 100%;
		text-transform: uppercase;
		color: white;
	}
	
	a {
		z-index: 1;
		position: absolute;
	}
	
	p {
		width: 100%;
		margin: 0;
		text-shadow: var(--shadow);
		font-weight: bold;
	}
	
	.heading, .buttonText {
		font-size: calc(var(--width) / 23);
	}
	
	.text {
		font-size: calc(var(--width) / 30);
	}
	
	.buttonText {
		position: absolute;
		bottom: calc(var(--width) / 90);
	}
	
	img {
		object-fit: cover;
		width: var(--width);
		height: calc(var(--width) / 16 * 9);
	}
	
		@media only screen and (max-width: 768px) {
		section {
			--width: 100vw;
		}
			
		.arrow {		
			display: none;
		}
			
		.dot {
			opacity: 1;
			transform: scale(2);
		}
			
			#buttons {
				width: 100%;
				display: flex;
				justify-content: space-around;
				padding-bottom: 2%;
			}
	}
</style>