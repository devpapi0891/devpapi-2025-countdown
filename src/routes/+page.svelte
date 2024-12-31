<script lang="ts">
  import Greetings from "./Greetings.svelte";
  import Countdown from "./Countdown.svelte";
  
  // function getCountdownDetails(targetDate: Date, message: string) {
  //   const now = new Date();
  //   // const targetDate = new Date('2025-01-01T00:00:00'); // for new year
  //   // const targetDate = new Date(now.getTime() + 10 * 1000); // For Testing. Comment this in production
  //   const timeDifference = targetDate.getTime() - now.getTime();

  //   // If the target date has passed
  //   if (timeDifference <= 0) {
  //     return {
  //       message: message,
  //       currentTime: now
  //     };
  //   }

  //   const days = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
  //   const hours = Math.floor((timeDifference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  //   const minutes = Math.floor((timeDifference % (1000 * 60 * 60)) / (1000 * 60));
  //   const seconds = Math.floor((timeDifference % (1000 * 60)) / 1000);

  //   return {
  //     // currentTime: now,
  //     days: days,
  //     hours: hours,
  //     minutes: minutes,
  //     seconds: seconds
  //   };
  // }

  function getCountdownDetails(targetDate: Date, message: string) {
    const now = new Date();
    const localTargetDate = new Date(targetDate.toLocaleString("en-US", { timeZone: Intl.DateTimeFormat().resolvedOptions().timeZone }));

    const timeDifference = localTargetDate.getTime() - now.getTime();

    // If the target date has passed
    if (timeDifference <= 0) {
      return {
        message: message,
        currentTime: now
      };
    }

    const days = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
    const hours = Math.floor((timeDifference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    const minutes = Math.floor((timeDifference % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((timeDifference % (1000 * 60)) / 1000);

    return {
      days: String(days).padStart(2, '0'),
      hours: String(hours).padStart(2, '0'),
      minutes: String(minutes).padStart(2, '0'),
      seconds: String(seconds).padStart(2, '0')
    };
  }


  let now = new Date();
  let targetDate: Date = new Date(now.getTime() + 119 * 1000);
  // let targetDate = new Date('2025-01-01T00:00:00');
  let message: string = "Happy New Year 2025";

  // Example usage
  setInterval(() => {
      countdown = getCountdownDetails(targetDate, message);
  }, 1000);

  let countdown = $state();
</script>


{#if countdown && (countdown as any).message}
  <Greetings message={(countdown as any).message} />
{:else}
  <Countdown countdown={countdown} />
{/if}

