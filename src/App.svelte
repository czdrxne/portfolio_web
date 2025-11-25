<script>
  import Preloader from "@components/Preloader.svelte";
  import Home from "@components/Home.svelte";
</script>

<Preloader />

<div id="smooth-wrapper" class="h-screen overflow-hidden bg-bg-pri cursor-default">
  <main id="smooth-content" class="w-full">
    <Home />
  </main>
</div>

