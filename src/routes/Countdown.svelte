<script lang="ts">
    import { onMount } from "svelte";

  let {
    countdown = $bindable()
  } = $props();

  let pingState = $state(false);

  onMount(() => {
    setInterval(() => {
    if ((countdown as any).days == 0 && 
      (countdown as any).hours == 0 && 
      (countdown as any).minutes == 0 && 
      (countdown as any).seconds <= 59) {
      pingState=true;  // Use .set() to update the state
    }
    }, 1000);
  })
  
  // $effect(() => {
  //   countdown;
  //   if ((countdown as any).days == 0 && 
  //     (countdown as any).hours == 0 && 
  //     (countdown as any).minutes == 0 && 
  //     (countdown as any).seconds <= 59) {
  //     pingState=true;  // Use .set() to update the state
  //   }
  // })
</script>

<section class="p-2 h-screen flex flex-col items-center justify-center space-y-12">
  <h1 
    class="font-extrabold text-lg sm:text-3xl md:text-5xl animate-pulseX
    bg-gradient-to-r from-blue-500 via-purple-500 to-pink-500 text-transparent bg-clip-text
    "
  >New Year Count Down</h1>
  {#if !pingState}
    <div class="grid grid-cols-4 gap-4 border-2 p-2 animate-pulse">
      {#if countdown}
        {#each Object.entries(countdown) as [key, value]}
          <div class="p-2 w-full border-2 rounded-md">
            <span class="text-xs md:text-xl font-medium capitalize">{key}</span>
            <div class="text-end aspect-square flex items-center justify-end text-3xl sm:text-7xl md:text-9xl">
              {String(value).padStart(2, '0')}
            </div>
          </div>
        {/each}
      {/if}
    </div>
  {:else}
    {#if countdown && (countdown as any).seconds}
    <div>
      <div class="p-2 w-full border-2X rounded-md animate-ping">
        <!-- <span class="text-xs md:text-xl font-medium capitalize">{key}</span> -->
        <div class="text-end aspect-square flex items-center justify-end text-3xl sm:text-7xl md:text-9xl">
          {String(countdown.seconds).padStart(2, '0')}
        </div>
      </div>
    </div>
    {/if}
  {/if}
</section>