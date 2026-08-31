<script lang="ts">
    import { onMount } from 'svelte';
    import led from '$lib/assets/led.jpg';
    import rotaryincoder from '$lib/assets/rotaryincoder.jpg';
    import transistor from '$lib/assets/transistor.jpg';
    import button from '$lib/assets/button.jpg';
    import resistor from '$lib/assets/resistor.jpg';
    import dcmotor from '$lib/assets/dcmotor.jpg';

    import { gsap } from 'gsap';
    import { ScrollTrigger } from 'gsap/ScrollTrigger';

    gsap.registerPlugin(ScrollTrigger);

    onMount(() => {
        gsap.to(".led", {
            scrollTrigger: {
                trigger: "body",
                start: "top top",
                markers: false,
            },
            y: -100,
            x: 50,
        });
    });

    onMount(() => {
        gsap.to(".rotaryincoder", {
            scrollTrigger: {
                trigger: "body",
                start: "top top",
                markers: false,
            },
            y: -100,
        });
    });

    onMount(() => {
        gsap.to(".transistor", {
            scrollTrigger: {
                trigger: "body",
                start: "top top",
                markers: false,
            },
            y: -100,
            x: -50,
        });
    });

    onMount(() => {
        gsap.to(".button", {
            scrollTrigger: {
                trigger: "body",
                start: "top top",
                markers: false,
            },
            y: -100,
            x: -50,
        });
    });

    onMount(() => {
        gsap.to(".resistor", {
            scrollTrigger: {
                trigger: "body",
                start: "top top",
                markers: false,
            },
            y: -100,
            x: 50,
        });
    });

    onMount(() => {
        gsap.to(".dcmotor", {
            scrollTrigger: {
                trigger: "body",
                start: "top top",
                markers: false,
            },
            y: -100,
        });
    });
    



    function confetti() {
        console.log('Confetti effect triggered!');
    }
</script>

<div class=" flex flex-col justify-center items-center w-full h-full">
    <header>
        
    </header>
    <h1 class="text-9xl font-climate py-6 text-center">Bulky</h1>
    <p class="text-2xl text-center bg-brat">Build a hardware project with 10+ of the same component and get an organizer!</p>

    <div class="grid grid-cols-5 w-full h-150 gap-4 p-10">
        <img src={led} alt='led' class="led w-50 absolute bottom-0 left-10"/>
        <img src={rotaryincoder} alt='rotary encoder' class="rotaryincoder w-50 absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2"/>
        <img src={transistor} alt='transistor' class="transistor w-50 absolute bottom-0 right-10"/> 
        <img src={button} alt='button' class="button w-50 absolute bottom-10 left-1/4"/>
        <img src={resistor} alt='resistor' class="resistor w-50 absolute bottom-5 right-1/4"/> 
        <img src={dcmotor} alt='dc motor' class="dcmotor w-50 absolute bottom-10 right-1/4"/>   
    </div>

    <p class="text-xl text-brat font-bold bg-gray-200 p-4">How this works</p>
    <ul>
        <li>Choose a component you have bulk of to excessively use in your project.</li>
        <li>Spend time designing and building your project.</li>
        <li>Get a grant to buy a proper organizer!</li>
    </ul>

    <p>Don't have hardware? Get a grant instead to build your project!</p>

    <h3>The point is to get rid of your hardware and make space for nicer hardware!</h3>

    <div class="bg-gray-200 p-4">
         <h2>What can I make?</h2>
         <h2>Hover the components above for idea!</h2>
    </div>
   
    <div class="bg-gray-200 p-4">
        <h2>Submission Guidelines</h2>
        <p>Track your design and build hours using Lapse or Journaling.</p>
        <p>Your git repository should contain all design files and scripts if necessary.</p>
        <p>Finally, submit here to get your grant!</p>
    </div>
    <div>
        <h2>Frequently Asked Questions</h2>

    </div>
    <footer class="flex flex-col justify-center items-center w-full h-full py-6 bg-gray-800 text-white">
        <p>Made with ❤️ by Selena</p>
        <p>Privacy & Terms</p>
        <p>Security Bounty</p>
    </footer>
     <footer class="flex flex-col justify-center items-center w-full h-full py-6 bg-gray-800 text-white">
        <p>Made with ❤️ by Selena</p>
        <p>Privacy & Terms</p>
        <p>Security Bounty</p>
    </footer>
     <footer class="flex flex-col justify-center items-center w-full h-full py-6 bg-gray-800 text-white">
        <p>Made with ❤️ by Selena</p>
        <p>Privacy & Terms</p>
        <p>Security Bounty</p>
    </footer>
     <footer class="flex flex-col justify-center items-center w-full h-full py-6 bg-gray-800 text-white">
        <p>Made with ❤️ by Selena</p>
        <p>Privacy & Terms</p>
        <p>Security Bounty</p>
    </footer>
     <footer class="flex flex-col justify-center items-center w-full h-full py-6 bg-gray-800 text-white">
        <p>Made with ❤️ by Selena</p>
        <p>Privacy & Terms</p>
        <p>Security Bounty</p>
    </footer>
</div>
