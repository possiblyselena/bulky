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
    
    let element = $state('');

    const imageMap: Record<string, string> = {
        led,
        rotaryincoder,
        transistor,
        button,
        resistor,
        dcmotor,
    };

    let particles: Array<{
        x: number;
        y: number;
        size: number;
        speedX: number;
        speedY: number;
        rotation: number;
        image: HTMLImageElement;
    }> = [];

    let animationId: number;
    let canvas: HTMLCanvasElement;
    let ctx: CanvasRenderingContext2D;

    onMount(() => {
        canvas = document.createElement('canvas');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        canvas.style.position = 'fixed';
        canvas.style.top = '0';
        canvas.style.left = '0';
        canvas.style.pointerEvents = 'none';
        canvas.style.zIndex = '9999';
        document.body.appendChild(canvas);
        ctx = canvas.getContext('2d')!;

    function createParticle(imageSrc: string) {
    const img = new Image();
    img.src = imageSrc;
    
    particles.push({
      x: Math.random() * canvas.width,
      y: -10,
      size: Math.random() * 30 + 20,
      speedX: (Math.random() - 0.5) * 4,
      speedY: Math.random() * 4 + 2,
      rotation: (Math.random() - 0.5) * 5,
      image: img,
    });
  }

  function updateParticle(p: typeof particles[0]) {
    p.x += p.speedX;
    p.y += p.speedY;
    p.x += Math.sin(p.y * 0.1) * Math.random() * 0.5;
  }

  function drawParticle(p: typeof particles[0]) {
    ctx.save();
    ctx.translate(p.x, p.y);
    ctx.rotate(p.rotation);
    
    if (p.image.complete) {
      ctx.drawImage(p.image, -p.size / 2, -p.size / 2, p.size, p.size);
    }
    
    ctx.restore();
  }

    function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        for (let i = particles.length - 1; i >= 0; i--) {
            updateParticle(particles[i]);
            drawParticle(particles[i]);
        if (particles[i].y > canvas.height + 20) {
            particles.splice(i, 1); 
        }
        }

        animationId = requestAnimationFrame(animate);
    }

        animate();

  return () => {
    window.removeEventListener("resize", () => {});
    cancelAnimationFrame(animationId);
    canvas.remove();
  };
});

    function confetti({element}: {element: string}) {
        if (!element || !imageMap[element]) return;
  
        for (let i = 0; i < 150; i++) {
            const img = new Image();
            img.src = imageMap[element];
    
            particles.push({
                x: Math.random() * window.innerWidth,
                y: -10,
                size: Math.random() * 30 + 20,
                speedX: (Math.random() - 0.5) * 4,
                speedY: Math.random() * 4 + 2,
                rotation: (Math.random() - 0.5) * 5,
                image: img,
            });
        }
    }
</script>

<div class=" flex flex-col justify-center items-center w-full h-full">
    <header class="flex flex-row justify-between items-center w-full h-10 bg-gray-200 text-black p-4">
        <p class="text-2xl font-bold">Hack Club</p>
        <p class="text-2xl font-bold">Submit</p>
    </header>
    <h1 class="text-9xl font-climate py-6 text-center">Bulky</h1>
    <p class="text-2xl text-center bg-brat p-1">Build a hardware project with 10+ of the same component and get an storage organizer!</p>

    <div class="grid grid-cols-5 w-full h-150 gap-4 p-10 relative">
        <img src={led} alt='led' class="led w-50 absolute bottom-0 left-10 cursor-pointer" on:click={() => { element = 'led'; confetti({element: 'led'}); }}/>
        <img src={rotaryincoder} alt='rotary encoder' class="rotaryincoder w-50 absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 cursor-pointer" on:click={() => { element = 'rotaryincoder'; confetti({element: 'rotaryincoder'}); }}/>
        <img src={transistor} alt='transistor' class="transistor w-50 absolute bottom-0 right-10 cursor-pointer" on:click={() => { element = 'transistor'; confetti({element: 'transistor'}); }}/> 
        <img src={button} alt='button' class="button w-50 absolute bottom-10 left-1/4 cursor-pointer" on:click={() => { element = 'button'; confetti({element: 'button'}); }}/>
        <img src={resistor} alt='resistor' class="resistor w-50 absolute bottom-5 right-1/4 cursor-pointer" on:click={() => { element = 'resistor'; confetti({element: 'resistor'}); }}/> 
        <img src={dcmotor} alt='dc motor' class="dcmotor w-50 absolute bottom-10 right-1/4 cursor-pointer" on:click={() => { element = 'dcmotor'; confetti({element: 'dcmotor'}); }}/>
    </div>
 
    <p class="text-2xl font-bold">{element}</p>

    <div class="grid grid-cols-2">
        <div>
            <p class="text-xl font-bold bg-gray-200 p-4 m-4">How this works</p>
            <ul class="p-4 text-lg">
                <li>❈ Choose a component you have bulk of to excessively use in your project.</li>
                <li>❈ Spend time designing and building your project.</li>
                <li> ❈Get a grant to buy a proper organizer!</li>
            </ul>
            <p>Don't have hardware? You can get a grant instead to build your project!</p>
        </div>
        <div>
            <p class="text-xl font-bold bg-gray-200 p-4 m-4">Submission Guidelines</p>
            <ul class="p-4 mx-4 text-lg">
                <li>❈ All progress must be documented with Lapse or Journaling.</li>
                <li>❈ Any files including schematics, code, and CAD designs must be included in your GitHub Repository.</li>
                <li> ❈Have a good readme.md file with a BOM of all components used (Really important if you need a grant!)</li>
                <li></li>
            </ul>
            <p>Submit your project here to get a grant!</p>
        </div>
    </div>
   

    <h3 class="text-2xl font-bold bg-brat p-4 m-4">The point is to get rid of your hardware and make space for nicer hardware!</h3>

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
