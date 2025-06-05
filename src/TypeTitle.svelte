<script>
	
	let visible = $state(false);

	function typewriter(node, { speed = .8 }) {
		const valid = node.childNodes.length === 1 && node.childNodes[0].nodeType === Node.TEXT_NODE;

		if (!valid) {
			throw new Error(`This transition only works on elements with a single text node child`);
		}

			const text = node.textContent;
			const duration = text.length / (speed * 0.03);
		
			return {
				duration,
				tick: (t) => {
					const i = Math.trunc(text.length * t);
					node.textContent = text.slice(0, i);
				}
		};
	}
	setTimeout(() => {
		visible = true;
	}, 500);
</script>

{#if visible}
	<h1 transition:typewriter>
		Martyn Vesey Web Development Portfolio
	</h1>
{/if}

<style>
	h1 {
		margin: 0;
		@media only screen and (max-width: 500px) {
			font-size: 24px;
		}
		@media only screen and (max-width: 350px) {
			font-size: 22px;
		}
	}
</style>