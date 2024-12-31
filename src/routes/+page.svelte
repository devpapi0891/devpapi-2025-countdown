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

  // function getCountdownDetails(targetDate: Date, message: string) {
  //   const now = new Date();
  //   const localTargetDate = new Date(targetDate.toLocaleString("en-US", { timeZone: Intl.DateTimeFormat().resolvedOptions().timeZone }));

  //   const timeDifference = localTargetDate.getTime() - now.getTime();

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
  //     days: String(days).padStart(2, '0'),
  //     hours: String(hours).padStart(2, '0'),
  //     minutes: String(minutes).padStart(2, '0'),
  //     seconds: String(seconds).padStart(2, '0')
  //   };
  // }

  function getCountdownDetails(targetDate: Date, message: string) {
    // Get the current time in local timezone
    const now = new Date();
    
    // Convert current time to UTC (user's local time in UTC)
    const utcNow = Date.UTC(now.getFullYear(), now.getMonth(), now.getDate(), now.getHours(), now.getMinutes(), now.getSeconds());

    // Ensure the target date is in UTC by using its ISO string representation
    const targetUtcDate = new Date(targetDate.toISOString()).getTime(); // This ensures targetDate is treated in UTC

    const timeDifference = targetUtcDate - utcNow;

    // If the target date has passed
    if (timeDifference <= 0) {
        return {
            message: message,
            currentTime: new Date(utcNow) // Return the UTC time for accurate timestamp
        };
    }

    // Calculate remaining time components
    const days = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
    const hours = Math.floor((timeDifference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    const minutes = Math.floor((timeDifference % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((timeDifference % (1000 * 60)) / 1000);

    // Return the formatted values
    return {
        days: String(days).padStart(2, '0'),
        hours: String(hours).padStart(2, '0'),
        minutes: String(minutes).padStart(2, '0'),
        seconds: String(seconds).padStart(2, '0')
    };
  }

  let targetDate = new Date('2025-01-01T00:00:00Z'); // January 1, 2025, at midnight UTC
  let message = "Happy New Year 2025!";
  // let countdownDetails = getCountdownDetails(targetDate, message);

  let countdown = $state();
  setInterval(() => {
    countdown = getCountdownDetails(targetDate, message);
  }, 1000);
</script>


{#if countdown && (countdown as any).message}
  <Greetings message={(countdown as any).message} />
{:else}
  <Countdown countdown={countdown} />
{/if}

