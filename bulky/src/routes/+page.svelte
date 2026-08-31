<script lang="ts">
    import { onMount } from 'svelte';
    import led from '$lib/assets/led.jpg';
    import rotaryincoder from '$lib/assets/rotaryincoder.jpg';
    import transistor from '$lib/assets/transistor.jpg';
    import { gsap } from 'gsap';
    import { ScrollTrigger } from 'gsap/ScrollTrigger';

    gsap.registerPlugin(ScrollTrigger);

    onMount(() => {
        gsap.to(".box", {
            scrollTrigger: ".box", // start the animation when ".box" enters the viewport (once)
            y: -100,
        });
    });

    function confetti() {
        console.log('Confetti effect triggered!');
    }
</script>

<div class=" flex flex-col justify-center w-full h-screen">
    <h1 class="text-7xl font-climate py-6 text-center">Bulky</h1>
    <p class="text-lg text-center">Build a hardware project with 10+ of the same component and get an organizer!</p>

    <div class="grid grid-cols-3 w-full h-full gap-4 relative">
        <img src={led} alt='led' class="box w-50 absolute bottom-0 left-10"/>
        <img src={rotaryincoder} alt='rotary encoder' class="box w-50 absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2"/>
        <img src={transistor} alt='transistor' class="box w-50 absolute bottom-0 right-10"/>  
    </div>

    <p class="box">How this works</p>
    <ul>
        <li>Choose a component you have bulk of to excessively use in your project.</li>
        <li>Spend time designing and building your project.</li>
        <li>Get a grant to buy a proper organizer!</li>
    </ul>

    <h1>Common Items that accumulate while you build hardware and Ideas for Them.</h1>

    <h2>LEDS</h2>
    <p>LED Cube</p>

    <p>Buttons</p>
    <p>Some wacky controller</p>

    <p>Switches</p>
    <p>Weird Macropad</p>

    <p>Transistors</p>
    <p>A puzzle</p>

    <h3>The point is to get rid of your hardware and make space for nicer hardware!</h3>

    <footer>
        <button onclick={confetti}>LED</button>
    </footer>
</div>
