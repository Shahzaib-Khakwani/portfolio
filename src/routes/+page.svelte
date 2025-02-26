<script>
    import { base } from "$app/paths";
    import { onMount } from "svelte";
    import { gsap } from 'gsap';
    import { fade } from 'svelte/transition';
    import { ScrollTrigger } from "gsap/ScrollTrigger";

    let leftCrumble ;
    let rightCrumble ;
    let websiteBadge;
    let LandingBadge;
    let BrandingBadge;
    let websiteHeading;
    let heroHeading
    let fireIcon;

    gsap.registerPlugin(ScrollTrigger);

    onMount( ()=> {
        const tl = gsap.timeline({defaults: {
            duration:.5,
        }})
        tl.from([websiteBadge, LandingBadge, BrandingBadge], {
            opacity: 0, 
            yPercent: 230,
            duration:1,
        }, '<')
        .from(heroHeading, {
            opacity: 0,
            yPercent: 70,
        },'<')
        .from(websiteHeading, {
            yPercent: -800,
        })
        .from(fireIcon,{
            scale: 0,
        })
        .from(leftCrumble, {
            xPercent: -100,
        },"<+=.2")
        .from(rightCrumble, {
            xPercent: 100,
        },"<+=.2")
        .to(websiteHeading, {
            rotate: '-7deg'
        },">")

        const panels = gsap.utils.toArray('.panel')

        gsap.to(panels,{
            xPercent: -100,
            opacity:0,
            stagger:0.8,
            scrollTrigger:{
                trigger:'.scrollContainer',
                start:"top top",
                end:'bottom top',
                scrub:true,
                pin:true,

            }
        })

        const scrollTl = gsap.timeline({
            scrollTrigger: {
                trigger: ".scrollSkillContainer",
                start:"+=80 top",
                end:"bottom",
                scrub:3,
                pin:".scrollSkillContainer",
                markers:false   ,
            }
        })

        scrollTl.to('.scroll-left-text',{
            xPercent:-20
        })
        scrollTl.to('.scroll-right-text',{
            xPercent:20
        },"<")

        const tileTL = gsap.timeline({
            scrollTrigger:{
                trigger:".tileContainer",
                start:"center bottom",
                end:"bottom top",
                // markers:true,
            }
        }).to('.brokenTile', {
            rotate:"2deg",
        })


        tileTL.to(".tileHello", {
            rotate:'8deg',
            duration:0.1,
            ease:"bounce.out",
            yoyo:true,
            repeat:-1,

        })

    })
</script>


<!-- Hero Section -->
<div class="min-h-screen w-full py-20 relative flex flex-col justify-center items-center bg-[#040229]">
        <h1 bind:this={heroHeading} class="text-white text-center font-semibold text-6xl">
            I Design The <p>
                Best
            </p>
        </h1>
        <div class="flex relative w-fit   justify-center ">
                <h2 bind:this={websiteHeading} class='text-black  font-bold text-5xl bg-[#F8CE68] px-5 py-2 mt-4'>WEBSITE</h2>
                <span class="absolute -top-4 -right-10">
                    <img bind:this={fireIcon} src="https://res.cloudinary.com/dmnwzu0xb/image/upload/v1668313548/rylic-assets/images/boom_wy6xl6.svg" alt="">
                </span>

        </div> 
        <div class="mt-5 flex justify-center ">
            <p transition:fade={300, 1500} class="text-[#B9B8C3] w-72  text-center leading-loose">
                We focus on <span class="text-white font-semibold"> Web</span> & <span class="text-white font-semibold">  Mobile</span> design, helping clients stand out by unique interfaces that sell the <span class="text-white font-semibold"> Brand</span> .
            </p>
        </div>
        
        <div class="flex  mt-4 gap-x-2 z-10">
            <img bind:this={websiteBadge} class="md:absolute md:top-[50%] md:left-[18%] md:h-12" src="{base}/images/website.svg" alt="">
            <img bind:this={LandingBadge} class="md:h-12" src="{base}/images/landing.svg" alt="">
            <img bind:this={BrandingBadge} class="md:absolute md:top-[50%] md:right-[18%] md:h-12 " src="{base}/images/branding.svg" alt="">

        </div>
        <div bind:this={leftCrumble} class="absolute top-[50%] left-0">
            <img src="https://res.cloudinary.com/dmnwzu0xb/image/upload/v16683553/rylic-assets/images/header-shape1_uganlc.svg" alt="">
        </div>
        <div class="absolute top-[50%] right-0">
            <img bind:this={rightCrumble} class="rightCumble" src="https://res.cloudinary.com/dmnwzu0xb/image/upload/v16683553/rylic-assets/images/header-shape2_lgcq9z.svg" alt="" srcset="">
        </div>
        
    </div>
<!-- End Heor Section -->


<!-- Services Cards -->
<div id="servicesContainer" class=" min-h-screen bg-[#D6CDC4] flex flex-col justify-center  pt-10  ">
    <h1 class="w-full text-center text-4xl font-black">
        What we offer!
    </h1>

    <div class="py-20 flex flex-col md:flex-row gap-y-20 md:gap-x-8  lg:justify-evenly justify-center items-center">
        <figure>
            <div class="bg-[#f3c75c] relative  rounded-2xl w-60 h-60" >
                <div class="overflow-hidden relative w-full h-full">
                    <svg class="w-54 h-54 absolute -top-[30%] left-[calc(50%-110px)] " viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
                        <path fill="#21B1DE" d="M47.2,-45.8C54,-29.1,47.5,-9.9,41.1,5.8C34.7,21.4,28.3,33.5,18.4,38.4C8.5,43.2,-5,40.9,-22.4,36.4C-39.8,31.9,-61.1,25.4,-68.5,10.5C-76,-4.3,-69.6,-27.4,-55.9,-45.6C-42.2,-63.8,-21.1,-77.2,-0.4,-76.9C20.2,-76.5,40.4,-62.4,47.2,-45.8Z" transform="translate(100 100)" />
                    </svg>

                    <h1 class="absolute top-[55%] left-[51%] -translate-x-1/2 text-center text-2xl font-bold">
                        Website Design
                    </h1>
                    </div>
                    <img
                    class="absolute w-24 h-24 -top-[15%] left-[calc(50%-50px)] animate-smooth-updown" 
                    src="{base}/images/earth.png" 
                    alt="nothing"
                    >
            </div>
            <p class="w-56 mt-5 text-start font-semibold ">Creating Multipage websites for different companies.</p>
        </figure>
        
        <figure>
            <p class="w-56 mb-8 text-start font-semibold ">Helping our Clients to establish an amazing brand with irresistible and strong visual elements.</p>
            <div class="bg-[#040229] relative  rounded-2xl w-60 h-60" >
                <div class="overflow-hidden relative w-full h-full">
                
                    <svg class="w-54 h-54 absolute -top-[40%] left-[calc(50%-110px)] " viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
                        <path fill="#0B32CE" d="M42.2,-9C51.6,15.1,53.9,46.2,37.4,60.2C21,74.2,-14.2,71.1,-37,53.8C-59.9,36.5,-70.4,5.1,-62.2,-17.4C-53.9,-39.9,-27,-53.5,-5.3,-51.8C16.4,-50.1,32.8,-33.1,42.2,-9Z" transform="translate(100 100)" />
                    </svg>

                    <h1 class="absolute top-[55%] left-[51%] -translate-x-1/2 text-center text-white text-2xl font-bold">
                        Performance
                        Website
                    </h1>
                    </div>
                    <img
                    class="absolute w-24 h-24 -top-[15%] left-[calc(50%-50px)] animate-smooth-updown" 
                    src="{base}/images/speaker.png" 
                    alt="nothing"
                    >
            </div>
        </figure>

        
        <figure>
            <div class="bg-[#ff6914] relative  rounded-2xl w-60 h-60" >
                <div class="overflow-hidden relative w-full h-full">
                    <svg class="w-84 h-84 absolute -top-[40%] left-[calc(50%-120px)] " viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
                        <path fill="#D3FF22" d="M47,-0.6C47,29,23.5,58.1,-1,58.1C-25.5,58.1,-51.1,29,-51.1,-0.6C-51.1,-30.2,-25.5,-60.4,-1,-60.4C23.5,-60.4,47,-30.2,47,-0.6Z" transform="translate(100 100)" />
                    </svg>
                    <h1 class="absolute top-[55%] left-[51%] -translate-x-1/2 text-center text-white text-2xl font-bold">
                        AI Agentic SaaS
                        
                    </h1>
                    </div>
                    <img
                    class="absolute w-24 h-24 -top-[15%] left-[calc(50%-50px)] animate-smooth-updown" 
                    src="{base}/images/pencil.png" 
                    alt="nothing"
                    >
            </div>
            <p class="w-56 mt-5 text-start font-semibold ">Experts are available for creating fast and dope landing page for your business like our website 😎</p>

        </figure>

        

    </div>
</div>
<!--End Services Cards -->

<!-- Divider -->
<div class="bg-[#D6CDC4] w-full ">
<div
class="mx-auto border-t-[3px] border-[#8B2C55] w-2/3  rounded-full"
>
</div>
</div>
<!-- End Divider -->


<!-- Horizental Scroll Project Gallery -->
<div class="scrollContainer h-screen w-full bg-[#D6CDC4]  relative flex justify-center py-[30px] items-center">

    <img 
    class="panel w-96 h-96 border-[10px] border-b-[30px] rotate-[-8deg] absolute z-40"
    src="{base}/images/back_page-0001.jpg" 
    alt="">
    <img 
    class="panel w-96 h-96 border-[10px] border-b-[30px] rotate-[10deg] absolute z-30"
    src="{base}/images/django_page-0001.jpg" 
    alt="">
    <img 
    class="panel w-96 h-96 border-[10px] border-b-[30px] rotate-[-12deg] absolute z-20"
    src="{base}/images/vision_page-0001.jpg" 
    alt="">
    <img 
    class="panel w-96 h-96 border-[10px] border-b-[30px] rotate-[14deg] absolute z-10"
    src="{base}/images/version.jpg" 
    alt="">

</div>
<!-- End Horizental Scroll Project Gallery -->

<!-- Skills Display -->
<div id="scrollSkillContainer" class="scrollSkillContainer min-h-screen w-full bg-[#040229] relative flex flex-col items-center justify-center overflow-hidden">
    <div class="scroll-left-text relative whitespace-nowrap inline-block transform will-change-transform">
        <h3 class="text-6xl font-black text-[#C0C0C9] ">GSAP | GSAP | GSAP | GSAP | GSAP | GSAP | GSAP | GSAP | GSAP | <span class="text-blue-500"> GSAP </span> | GSAP | GSAP | GSAP | GSAP | GSAP | GSAP | GSAP | GSAP </h3>
    </div>
    <div class="scroll-right-text relative whitespace-nowrap inline-block transform will-change-transform">
        <h3 class="text-6xl font-black text-[#C0C0C9] ">LangChain | LangChain | LangChain | LangChain |<span class="text-green-500"> LangChain </span>| LangChain | LangChain | LangChain | LangChain |</h3>
    </div>
    <div class="scroll-left-text relative whitespace-nowrap inline-block transform will-change-transform">
        <h3 class="text-6xl font-black text-[#C0C0C9] "> SvelteKit | SvelteKit | SvelteKit | SvelteKit | SvelteKit | SvelteKit |<span class="text-red-500"> SvelteKit </span>| SvelteKit | SvelteKit | SvelteKit | SvelteKit | SvelteKit | SvelteKit |</h3>
    </div>
    <div class="scroll-right-text relative whitespace-nowrap inline-block transform will-change-transform">
        <h3 class="text-6xl font-black text-[#C0C0C9] "> Python | Python | Python | Python | Python |<span class="text-yellow-500"> Python </span>| Python | Python | Python | Python | Python </h3>
    </div>

</div>
<!-- End Skills Display -->

<!-- Contact Display -->
<div id="tileContainer" class="tileContainer h-screen w-full bg-[#040229] relative flex flex-col items-center justify-center py-10">
    <div class="tileHello w-36 h-36 md:w-48 md:h-48 absolute top-[5%] left-[10%]">
        <img 
        src="https://res.cloudinary.com/dmnwzu0xb/image/upload/v1669354656/new-images/hello_aen4ug.png"
        alt="">
    </div>
    <div class=" w-full flex flex-col items-center justify-center gap-y-2 ">
        <a 
        href="https://github.com/Shahzaib-Khakwani/"
        target="_blank"
        rel="noopener noreferrer"
        class="bg-white rounded-xl text-black w-2/3 md:w-1/2 p-4 text-center font-bold "
        >GitHub</a>
        <a 
        href="https://www.linkedin.com/in/shahzaib-khakwani-18b976268?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app" 
        target="_blank" 
        rel="noopener noreferrer"
        class="brokenTile bg-[#D2D2D2] rounded-xl text-black w-2/3 md:w-1/2 p-4 text-center font-bold"
        >LinkedIn</a>
        <a 
        href="https://www.kaggle.com/shahzaibkhakwani"
        target="_blank"
        rel="noopener noreferrer"
        class="bg-white rounded-xl text-black w-2/3 md:w-1/2 p-4 text-center font-bold "
        >Kaggle</a>
        
    </div>
    <div>

    </div>
</div>
<!-- End Contact Display -->



<style>
    @keyframes smoothUpDown {
        0%, 100% {
        transform: translateY(0);
        }
        50% {
        transform: translateY(-5px);
        }
    }

  .animate-smooth-updown {
    animation: smoothUpDown 2s ease-in-out infinite;
  }
</style>

