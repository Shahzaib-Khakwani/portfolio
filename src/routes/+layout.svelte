<script>
	import '../app.css';
	import { onMount } from "svelte";
	import { gsap } from "gsap";
	import { goto } from "$app/navigation";
	import { navigating } from "$app/stores";
	import Loader from "$lib/components/loader.svelte";
	import { isLoading } from "$lib/stores/loading";
    import { ScrollTrigger } from "gsap/ScrollTrigger";
    import { fade, slide, fly } from 'svelte/transition';


	let { children } = $props();
	let navbarRef;
	let isMounted =$state(false);
	let isNavbar =$state(false);

    gsap.registerPlugin(ScrollTrigger);


	onMount(()=>{
		handleLoad()
	})

	const handleLoad = ()=> {
		setTimeout(() => {
			$isLoading = false;
			isMounted = true;

                gsap.from(navbarRef, {
                    yPercent: -200,
                    duration: 1,
                    ease: "power2.out",
                    delay:.1,
                });
            

		}, 4000);
	}

	const toggleMenu = () => {
        isNavbar = !isNavbar;
		// const menu = document.getElementById('navbar-sticky');
		// menu.classList.toggle('hidden');
	}
    const handleNavigation = async (url)=> {
        toggleMenu();
        await new Promise(resolve => setTimeout(resolve, 500));
        goto(url);
    }

</script>


<div class="relative min-h-screen bg-[#040229]">
    {#if $isLoading}
    <div in:fade out:fade class="fixed inset-0 z-50">
        <Loader />
    </div>
    {:else if  isMounted} 
{#if isNavbar}
<div in:slide out:slide class="absolute z-30 h-screen w-full bg-black flex flex-col justify-center items-center">
<ul class="flex flex-col p-4 text-center text-3xl gap-y-8 font-medium     ">		
    <li>
    <button in:fly={{x:-400, delay:500, duration:400}} onclick={()=>handleNavigation('#scrollSkillContainer')} class="block py-2 px-3 text-gray-900 rounded-sm hover:bg-gray-100 md:hover:bg-transparent md:hover:text-blue-700 md:p-0 md:dark:hover:text-blue-500 dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700 transition duration-250">About</button>
    </li>
    <li>
    <button in:fly={{x:-400, delay:600, duration:400}} onclick={()=>handleNavigation('#servicesContainer')} class="block py-2 px-3 text-gray-900 rounded-sm hover:bg-gray-100 md:hover:bg-transparent md:hover:text-blue-700 md:p-0 md:dark:hover:text-blue-500 dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700 transition duration-250">Services</button>
    </li>
    <li>
    <button in:fly={{x:-400, delay:700, duration:400}} onclick={()=>handleNavigation('#tileContainer')} class="block py-2 px-3 text-gray-900 rounded-sm hover:bg-gray-100 md:hover:bg-transparent md:hover:text-blue-700 md:p-0 md:dark:hover:text-blue-500 dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700 transition duration-250">Contact</button>
    </li>
</ul>
</div>  
{/if}

<nav bind:this={navbarRef} class="bg-transparent absolute  w-full z-40 top-2 start-0 ">
	<div class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
	<a href="/" class="flex items-center space-x-3 text-white font-black text-4xl rtl:space-x-reverse">
		SHAHZAIB
        <!-- <img src="https://res.cloudinary.com/dmnwzu0xb/image/upload/v1670118902/new-images/logo_pd3pd9.svg" class="h-8" alt="Flowbite Logo"> -->
	</a>
	<div class="flex md:order-2 space-x-3 md:space-x-0 rtl:space-x-reverse">
		<!-- <button type="button" class="hidden bg-[#F0C46D] hover:bg-[#eeba55] transition duration-150 text-[#000000] font-bold text-xl rounded-3xl md:block text-white bg-blue-700 px-5 py-3">
			<svg xmlns="http://www.w3.org/2000/svg" class="inline mr-3" width="30" height="30" fill="none" viewBox="0 0 30 30">
				<path fill="#fff" d="M5.717 5.72a13.13 13.13 0 0 0-2.822 4.198 13.237 13.237 0 0 0-1.028 5.142 13.094 13.094 0 0 0 13.122 13.066h.062a13.112 13.112 0 0 0 1.616-.107c2.906-.374 5.766-1.3 8.696-1.3.744 0 1.348-.603 1.348-1.347 0-2.928.923-5.787 1.298-8.69.07-.537.106-1.077.108-1.62a13.124 13.124 0 0 0-1.005-5.12 12.997 12.997 0 0 0-2.786-4.184 13.094 13.094 0 0 0-9.273-3.879h-.058c-1.76 0-3.472.343-5.083 1.02a13.037 13.037 0 0 0-4.195 2.82Z"></path>
				<path fill="#6A6A6A" d="M9.551 16.64c.882 0 1.594-.732 1.594-1.64 0-.908-.712-1.64-1.594-1.64-.882 0-1.594.732-1.594 1.64-.003.908.712 1.64 1.594 1.64Zm5.449 0c.882 0 1.594-.732 1.594-1.64 0-.908-.712-1.64-1.594-1.64-.882 0-1.594.732-1.594 1.64.003.908.715 1.64 1.594 1.64ZM22.043 15c0 .216-.041.429-.121.628a1.64 1.64 0 0 1-.346.532 1.591 1.591 0 0 1-.517.356 1.553 1.553 0 0 1-1.737-.356 1.682 1.682 0 0 1 0-2.32 1.57 1.57 0 0 1 1.127-.48c.423 0 .828.172 1.127.48.3.308.467.725.467 1.16Z"></path>
			</svg>
			Get started
		</button> -->


		<button onclick={toggleMenu} data-collapse-toggle="navbar-sticky" type="button" class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-gray-500 rounded-lg  hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600" aria-controls="navbar-sticky" aria-expanded="false">
			<span class="sr-only">Open main menu</span>
			<svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 17 14">
				<path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 1h15M1 7h15M1 13h15"/>
			</svg>
		</button>
        
  </nav>
  
  <main class="overflow-x-hidden">
	  {@render children()}
  </main>



<footer class="bg-white dark:bg-gray-900">
    <div class="mx-auto w-full max-w-screen-xl p-4 py-6 lg:py-8">
        <div class="md:flex justify-center">
         
          <div class="grid grid-cols-2 gap-8 sm:gap-6 sm:grid-cols-3">
             
              <div>
                  <h2 class="mb-6 text-sm font-semibold text-gray-900 uppercase dark:text-white">Follow us</h2>
                  <ul class="text-gray-500 dark:text-gray-400 font-medium">
                      <li class="mb-4">
                          <a target="_blank" href="https://github.com/Shahzaib-Khakwani/" class="hover:underline ">Github</a>
                      </li>
                      <li>
                          <a 
                            target="_blank" 
                            href="https://www.linkedin.com/in/shahzaib-khakwani-18b976268?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app"
                            class="hover:underline">Discord</a>
                      </li>
                  </ul>
              </div>
             
          </div>
      </div>
      <hr class="my-6 border-gray-200 sm:mx-auto dark:border-gray-700 lg:my-8" />
      <div class="sm:flex sm:items-center sm:justify-between">
          <span class="text-sm text-gray-500 sm:text-center dark:text-gray-400">© 2025 <a href="https://flowbite.com/" class="hover:underline">Shahzaib™</a>. All Rights Reserved.
          </span>
          <div class="flex mt-4 sm:justify-center sm:mt-0">
              
              
             
              <a target="_blank" href="https://github.com/Shahzaib-Khakwani/" class="text-gray-500 hover:text-gray-900 dark:hover:text-white ms-5">
                  <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 20 20">
                        <path fill-rule="evenodd" d="M10 .333A9.911 9.911 0 0 0 6.866 19.65c.5.092.678-.215.678-.477 0-.237-.01-1.017-.014-1.845-2.757.6-3.338-1.169-3.338-1.169a2.627 2.627 0 0 0-1.1-1.451c-.9-.615.07-.6.07-.6a2.084 2.084 0 0 1 1.518 1.021 2.11 2.11 0 0 0 2.884.823c.044-.503.268-.973.63-1.325-2.2-.25-4.516-1.1-4.516-4.9A3.832 3.832 0 0 1 4.7 7.068a3.56 3.56 0 0 1 .095-2.623s.832-.266 2.726 1.016a9.409 9.409 0 0 1 4.962 0c1.89-1.282 2.717-1.016 2.717-1.016.366.83.402 1.768.1 2.623a3.827 3.827 0 0 1 1.02 2.659c0 3.807-2.319 4.644-4.525 4.889a2.366 2.366 0 0 1 .673 1.834c0 1.326-.012 2.394-.012 2.72 0 .263.18.572.681.475A9.911 9.911 0 0 0 10 .333Z" clip-rule="evenodd"/>
                  </svg>
                  <span class="sr-only">GitHub account</span>
              </a>
              <a target="_blank" href="https://www.linkedin.com/in/shahzaib-khakwani-18b976268?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app" class="text-gray-500 hover:text-gray-900 dark:hover:text-white ms-5">
                  <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M10 0a10 10 0 1 0 10 10A10.009 10.009 0 0 0 10 0Zm6.613 4.614a8.523 8.523 0 0 1 1.93 5.32 20.094 20.094 0 0 0-5.949-.274c-.059-.149-.122-.292-.184-.441a23.879 23.879 0 0 0-.566-1.239 11.41 11.41 0 0 0 4.769-3.366ZM8 1.707a8.821 8.821 0 0 1 2-.238 8.5 8.5 0 0 1 5.664 2.152 9.608 9.608 0 0 1-4.476 3.087A45.758 45.758 0 0 0 8 1.707ZM1.642 8.262a8.57 8.57 0 0 1 4.73-5.981A53.998 53.998 0 0 1 9.54 7.222a32.078 32.078 0 0 1-7.9 1.04h.002Zm2.01 7.46a8.51 8.51 0 0 1-2.2-5.707v-.262a31.64 31.64 0 0 0 8.777-1.219c.243.477.477.964.692 1.449-.114.032-.227.067-.336.1a13.569 13.569 0 0 0-6.942 5.636l.009.003ZM10 18.556a8.508 8.508 0 0 1-5.243-1.8 11.717 11.717 0 0 1 6.7-5.332.509.509 0 0 1 .055-.02 35.65 35.65 0 0 1 1.819 6.476 8.476 8.476 0 0 1-3.331.676Zm4.772-1.462A37.232 37.232 0 0 0 13.113 11a12.513 12.513 0 0 1 5.321.364 8.56 8.56 0 0 1-3.66 5.73h-.002Z" clip-rule="evenodd"/>
                </svg>
                  <span class="sr-only">LinkedIn account</span>
              </a>
          </div>
      </div>
    </div>
</footer>
{/if} 

</div>