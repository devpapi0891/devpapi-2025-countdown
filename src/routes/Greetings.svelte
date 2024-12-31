<script lang="ts">
  let {
    message = $bindable()
  } = $props();
</script>

<section 
  class="p-2 h-screen flex flex-col items-center justify-center space-y-12 relative"
>
  <img 
    src="./new-years-day-1134.gif" 
    alt="fireworks"
    class="absolute inset-0 object-cover w-full h-full opacity-95 -z-10 animate-pulse"
  >

  <!-- Message -->
  <div
    class="pb-[10%]"
  >
    <div
      class="flex justify-center w-full"
    >
      <img 
        src="./dancing-chick.gif" 
        alt="dancing-chick"
        class="w-24 md:w-48"
      >
    </div>
    <h1
      class="font-bold text-5xl sm:text-5xl md:text-8xl text-center"
      style="text-shadow: 2px 2px 0 #000;"
    >{message}</h1>
  </div>

  <!-- DANCERS -->
  <div
    class="flex evenly gap-2 absolute w-full bottom-0 overflow-hidden"
  >
    {#each Array(8) as _}
      <img 
        src="./dancing1.gif" 
        alt="dancer"
        class="w-32 md:w-64"
      >
    {/each}
  </div>
</section>