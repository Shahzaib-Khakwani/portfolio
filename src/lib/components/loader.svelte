<script>
    import { onMount } from "svelte";
    import { fade, scale } from "svelte/transition";

    let loadingText = ["Shahzaib","Animation", "AI agents", "GSAP", "PORTFOLIO","Website","Animation", "AI agents", "GSAP", "PORTFOLIO","Shahzaib"];
    let currentTextIndex = $state(0);
    let textChangeIntervel;

    onMount(() => {
        textChangeIntervel = setInterval(()=>{
            currentTextIndex = (currentTextIndex + 1) % loadingText.length;
        }, 200);

        return () => {
            clearInterval(textChangeIntervel);
        }
    })

</script>



  <div class="h-screen w-full bg-[#040229] flex justify-center items-center">
    <p class="text-6xl md:text-9xl text-white font-black" in:fade out:fade>
      {loadingText[currentTextIndex]}
    </p>
  </div>
