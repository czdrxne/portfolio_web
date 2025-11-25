<script>
	import { onMount } from "svelte";

	let barsCount = 10;

	onMount(async() => {
    const { default: gsap } = await import("gsap");
    const timeline = gsap.timeline({ delay: 0.3 }) // MILISECONDS TIMELINE DELAY

		
		const mq = window.matchMedia("(max-width: 640px)");
		const update = () => barsCount = mq.matches ? 5 : 10;
		update();
		mq.addEventListener("change", update);

		// TEXT ANIMATION: INTRO
		timeline.fromTo(
			".logo span",
			{
				y: 100,
				opacity: 0,
				visibility: "hidden"
			},
			{
				y: 0,
				opacity: 1,
				visibility: "visible",
				duration: 0.15,
				ease: "power2.out",
				stagger: 0.03
			}
		)

		// ANIMATION: DELAY
		timeline.to({}, { duration: 0.5 })

		// TEXT ANIMATION: OUTRO
		timeline.to(
			".logo span",
			{
				opacity: 0,
				duration: 0.5,
				ease: "power2.in"
			}
		)

		// OBJECT ANIMATION: INTRO / OUTRO
		timeline.to(
			".bars",
			{
				y: "100%",
				duration: 1,
				ease: "power2.out",
				stagger: 0.07,
				onComplete: () => {
					document.querySelector(".preloader").style.display = "none";
				}
			}
		)
	})
</script>

<div class="preloader fixed flex inset-0 z-[1000] bg-none pointer-events-none">
	{#each Array(barsCount) as _, i}
		<div class="bg-white outline-hidden border-hidden bars h-full w-full translate-y-0"></div>
	{/each}

	<p class="logo flex text-[4.4rem] sm:text-[25vw] lg:text-[16vw] sm:gap-1 font-primary text-center absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 leading-none overflow-hidden tracking-tight text-black">
    {#each "CZDRXNE".split("") as letter}
      <span class="inline-block translate-y-full opacity-0 invisible">{letter}</span>
    {/each}
  </p>

</div>