<script lang="ts">
    import { onMount } from 'svelte';
    import led from '$lib/assets/led.png';
    import rotaryincoder from '$lib/assets/rotaryincoder.png';
    import transistor from '$lib/assets/transistor.png';
    import button from '$lib/assets/button.png';
    import dcmotor from '$lib/assets/dcmotor.png';
    import accordionitem from '$lib/components/accordionitem.svelte';

    import { gsap } from 'gsap';
    import { ScrollTrigger } from 'gsap/ScrollTrigger';
    import Accordionitem from '$lib/components/accordionitem.svelte';

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

    const imageMap: Record<string, string> = {
        led,
        rotaryincoder,
        transistor,
        button,
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

<div class="flex flex-col justify-center items-center w-full h-full">
    <header class="flex flex-row justify-between items-center w-full h-10 text-black py-6 m-3 pr-2 ">
        <a href="https://hackclub.com/"><img src="https://assets.hackclub.com/flag-orpheus-left-bw.svg" class="w-50 pt-10"/></a>
        <a href="https://forms.hackclub.com/bulky-submit" class="text-2xl font-bold border border-black p-3">Submit</a>
    </header>
    <h1 class="text-9xl font-climate py-6 text-center">Bulky</h1>
    <p class="text-2xl text-center bg-brat p-1">Build a hardware project with 10+ of the same component and get an storage organizer!</p>
    <p class="p-2 text-xl underline">Join <a href="https://hackclub.enterprise.slack.com/archives/C0BURQY9JN4">#bulky</a> to start!</p>

    <div class="grid grid-cols-5 w-full h-150 gap-4 p-10 relative">
        <img src={led} alt='led' class="led w-50 absolute bottom-0 left-10 cursor-pointer" on:click={() => { confetti({element: 'led'}); }}/>
        <img src={rotaryincoder} alt='rotary encoder' class="rotaryincoder w-50 absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 cursor-pointer" on:click={() => {confetti({element: 'rotaryincoder'}); }}/>
        <img src={transistor} alt='transistor' class="transistor w-50 absolute bottom-0 right-10 cursor-pointer" on:click={() => { confetti({element: 'transistor'}); }}/> 
        <img src={button} alt='button' class="button w-50 absolute bottom-10 left-1/4 cursor-pointer" on:click={() => { confetti({element: 'button'}); }}/>
        <img src={dcmotor} alt='dc motor' class="dcmotor w-50 absolute bottom-10 right-1/4 cursor-pointer" on:click={() => { confetti({element: 'dcmotor'}); }}/>
    </div>


    <div class="grid grid-cols-2">
        <div>
            <p class="text-xl font-bold bg-gray-200 p-4 m-2">How this works</p>
            <ul class="px-4 text-lg">
                <li class="p-2">❈ Choose a component you have bulk of to excessively use in your project.</li>
                <li class="p-2">❈ Track your time designing and building your project.</li>
                <li class="p-2">❈ Get a grant to buy a proper organizer!</li>
            </ul>
            <p class="p-2 px-6 text-lg font-bold">Don't have hardware? You can get a grant instead to build your project!</p>
        </div>
        <div>
            <p class="text-xl font-bold bg-gray-200 p-4 m-2">Submission Guidelines</p>
            <ul class="px-4 text-lg">
                <li class="p-2">❈ All progress must be documented with <a href="https://lapse.hackclub.com/" class="underline">Lapse</a>.</li>
                <li class="p-2">❈ Any files including schematics, code, and CAD designs must be included in your GitHub Repository.</li>
                <li class="p-2">❈ Have a good readme.md file with a BOM of all components used - really important if you need a grant!</li>
            </ul>
        </div>
    </div>
   

    <h3 class="text-2xl font-bold bg-brat p-4 m-4">The point is to get rid of your bulk hardware and make space for better hardware!</h3>

    <div class="text-lg bg-gray-200 flex flex-col justify-center items-center p-4 m-4">
         <h2>What can I make?</h2>
         <h2>I'll be posting ideas in <a class="hover:underline" href="https://hackclub.enterprise.slack.com/archives/C0BURQY9JN4">#bulky</a> and maybe even create bounties...</h2>
    </div>

    <div>
        <h2 class="grid justify-center items-center text-xl font-bold pt-10">Frequently Asked Questions</h2>
        <div class="grid grid-cols-2 p-4 m-4 gap-2">
            <Accordionitem title="What is Bulky?">
                <p class="text-md">Bulky is a You Ship, We Ship program where you design a hardware project with excessive amounts of the same component to earn a proper storage organizer!</p>
            </Accordionitem>
            <Accordionitem title="What is Hack Club?">
                <p class="text-md">Hack Club is a 501(c)(3) nonprofit and network of 100k+ technical high schoolers. We believe you learn best by building, so we’re creating community and providing grants so you can make awesome projects.</p>
            </Accordionitem>
            <Accordionitem title="Who can particpate?">
                <p class="text-md">Ages 13-18 inclusive can participate in Bulky.</p>
            </Accordionitem>
            <Accordionitem title="When is the deadline?">
                <p class="text-md">The deadline for both design and build is October 2nd, 11:59 PM EST.</p>
            </Accordionitem>
            <Accordionitem title="How do I track my hours?">
                <p class="text-md">For both design and build hours, you can use Lapse!</p>
            </Accordionitem>
            <Accordionitem title="What storage organizer can I get?">
                <p class="text-md">It's dependent on your hours tracked! I recommend getting a <a href="https://www.amazon.com/Akro-Mils-10144-20-Inch-16-Inch-Hardware/dp/B003P2UOCO/ref=sr_1_7?crid=P9MGASZLXFVX&dib=eyJ2IjoiMSJ9.wGfIJ7Npm9R-npky_ZAtdNIkmx91C7IgUo5EvcUWZR_HDUxMliir2ZoRGfxpuor9unTLD8tetWfSgrr1oFpoQ-qfP3Ms5Xq-3BBMQwAerAjchiX3PDTRAlGq1Wf3Tsw8TB8PsUrMAPpMkpq33DKFewV8WYz3gBG9RUGsEUFh--YI8Hw2USEJHodAISTi9EUiKFOwH_C899RuliwZfW3TyfGA3RwbwBwcGf6ZgwMoBbQHGlqTcPg7gV47_4C0nj3al2S2Q0pfOuzT-6ZnnTaLyfkCJS9xKcS63Ij49if_R1w.0sG6UZ7DDvrEyJ8H4dcqe3SsE9XV6adWctBOHqAPkm8&dib_tag=se&keywords=bin%2Borganizer&qid=1788286872&sprefix=bin%2Borganizer%2Caps%2C115&sr=8-7&th=1" class="hover:underline">plastic bin cabinet</a> or the <a href="https://www.amazon.com/Jack-Boss-Transparent-34-Compartments-Accessories/dp/B0CZDJNV19/ref=sr_1_2?crid=3JLRE2JHIU0EZ&dib=eyJ2IjoiMSJ9.2j8a7mkV4onyHodjI_DLTxLRN6XCoq3RdDESGmHvSmo83X5kjKP8eaYOxo8pXFyULTkrziir7SSz1HGY0JMUoV1sthd1R9mfJsdqnongzy0Vae6OpdUpns42rsuRD-N2hzXB1MgEGKsUanSNwSzMFJO5LxPyhtHm1Tnd79FswabUch4vdUpuTNuYv1OOOo2RPVrDxdbu-HnZWHdPOs0ySjG1zR31j5WMMxzVC4sLmTXs8d_KCX20D5fSSOcNTE3r4sQhDOS9WcTVUtinyVIj5DvVRHl_PFCEuT7TXNmQB04.PMEqEX7KQ8mJsjJzYU0hSD7lGAUzzskGyMJ2MA4ydPs&dib_tag=se&keywords=small%2Bbin%2Borganizer%2Bportable&qid=1788287027&sprefix=small%2Bbin%2Borganizer%2Bportabl%2Caps%2C122&sr=8-2&th=1" class="hover:underline">portable tool box</a>.</p>
            </Accordionitem>
            <Accordionitem title="I've designed the hardware, but I need a couple of components to finish it. Can I get a grant?">
                <p class="text-md">You should have most of the parts for your project, but we can give you a grant to up to 25$ to get the remaining components.</p>
            </Accordionitem>    
        </div> 
    </div>
    <footer class="flex flex-col justify-center items-center w-full h-full py-6 bg-gray-800 text-white">
        <p>Made with ❤️ by Selena</p>
        <div class="grid grid-cols-2 gap-4">
            <a class="text-brat hover:underline" href="https://forms.hackclub.com/bounty">Fufillment Bounty</a>
            <a class="text-brat hover:underline" href="https://hackclub.com/privacy-and-terms">Privacy & Terms</a>
        </div>
    </footer>
</div>
