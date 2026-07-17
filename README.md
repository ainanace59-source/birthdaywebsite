<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy Birthday ✨</title>
  
  <!-- CDN Links for Design and Functionality -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.3/dist/confetti.browser.min.js"></script>

  <style>
    /* Elegant Typography Imports */
    @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400..900;1,400..900&display=swap');
    @import url('https://api.fontshare.com/v2/css?f[]=satoshi@300,400,500,700&display=swap');

    /* Global Base Reset & Scroll behavior */
    body {
      font-family: 'Satoshi', sans-serif;
      background-color: #0c0a09;
      overflow-x: hidden;
      margin: 0;
      padding: 0;
      user-select: none;
    }

    .font-serif-display {
      font-family: 'Playfair Display', serif;
    }

    /* Layer 1: Animated Aurora Background Circles */
    @keyframes breathing {
      0%, 100% {
        transform: translate(0, 0) scale(1);
      }
      25% {
        transform: translate(4%, -6%) scale(1.08);
      }
      50% {
        transform: translate(-5%, 4%) scale(0.92);
      }
      75% {
        transform: translate(3%, 5%) scale(1.05);
      }
    }

    .aurora-circle {
      position: absolute;
      border-radius: 50%;
      filter: blur(130px);
      mix-blend-mode: screen;
      pointer-events: none;
      will-change: transform;
    }

    .aurora-1 {
      background: hsla(333, 70%, 55%, 0.3);
      width: 55vw;
      height: 55vw;
      top: -10%;
      left: -10%;
      animation: breathing 24s infinite ease-in-out;
    }

    .aurora-2 {
      background: hsla(282, 82%, 54%, 0.22);
      width: 65vw;
      height: 65vw;
      bottom: -15%;
      right: -5%;
      animation: breathing 28s infinite ease-in-out reverse;
    }

    .aurora-3 {
      background: hsla(210, 89%, 60%, 0.22);
      width: 50vw;
      height: 50vw;
      top: 30%;
      right: 15%;
      animation: breathing 32s infinite ease-in-out 2s;
    }

    .aurora-4 {
      background: hsla(35, 90%, 60%, 0.18);
      width: 45vw;
      height: 45vw;
      bottom: 25%;
      left: 10%;
      animation: breathing 26s infinite ease-in-out 4s reverse;
    }

    /* Glassmorphic Styles */
    .glass-card {
      background: rgba(12, 10, 9, 0.45);
      backdrop-filter: blur(24px);
      -webkit-backdrop-filter: blur(24px);
      border: 1px solid rgba(255, 255, 255, 0.08);
      box-shadow: 0 30px 70px rgba(0, 0, 0, 0.65);
    }

    /* Title text gradients */
    .text-gradient {
      background: linear-gradient(135deg, #ffffff 0%, #ffd1df 40%, #fecdd3 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    /* Custom Button Glow and States */
    .gradient-btn {
      background: linear-gradient(135deg, #ec4899 0%, #e11d48 100%);
      box-shadow: 0 4px 20px rgba(236, 72, 153, 0.35);
      transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .gradient-btn:hover {
      transform: translateY(-3px) scale(1.05);
      box-shadow: 0 8px 30px rgba(236, 72, 153, 0.6);
    }

    .gradient-btn:active {
      transform: translateY(-1px) scale(0.98);
      box-shadow: 0 2px 10px rgba(236, 72, 153, 0.3);
    }

    /* Polaroid Layout with 3D Space perspective */
    .perspective-container {
      perspective: 1200px;
    }

    .polaroid {
      transform-style: preserve-3d;
      will-change: transform;
    }

    /* Heart pulse effect for welcome screen */
    @keyframes heartbeat {
      0% { transform: scale(1); filter: drop-shadow(0 0 10px rgba(236, 72, 153, 0.4)); }
      25% { transform: scale(1.1); filter: drop-shadow(0 0 25px rgba(236, 72, 153, 0.8)); }
      40% { transform: scale(1); filter: drop-shadow(0 0 10px rgba(236, 72, 153, 0.4)); }
      55% { transform: scale(1.1); filter: drop-shadow(0 0 25px rgba(236, 72, 153, 0.8)); }
      100% { transform: scale(1); filter: drop-shadow(0 0 10px rgba(236, 72, 153, 0.4)); }
    }

    .heart-beat {
      animation: heartbeat 2.2s infinite ease-in-out;
    }
  </style>
</head>
<body class="min-h-screen flex flex-col justify-between items-center relative text-stone-200 p-4 select-none">

  <!-- ================= LAYERS 1 & 2: BACKGROUNDS ================= -->
  
  <!-- Layer 1: Simulated Aurora System -->
  <div class="fixed inset-0 w-full h-full overflow-hidden -z-30 pointer-events-none bg-[#0c0a09]">
    <div class="aurora-circle aurora-1"></div>
    <div class="aurora-circle aurora-2"></div>
    <div class="aurora-circle aurora-3"></div>
    <div class="aurora-circle aurora-4"></div>
  </div>

  <!-- Layer 2: 3D Floating Hearts Canvas -->
  <canvas id="canvas3d" class="fixed inset-0 w-full h-full -z-20 pointer-events-none"></canvas>


  <!-- ================= TOP FIXED PROGRESS BAR ================= -->
  <div class="fixed top-6 left-1/2 -translate-x-1/2 w-64 h-2 rounded-full bg-white/5 border border-white/5 backdrop-blur-md overflow-hidden z-50">
    <div id="progress-bar" class="h-full w-1/5 bg-gradient-to-r from-pink-500 via-rose-500 to-red-500 rounded-full transition-all duration-500"></div>
  </div>


  <!-- ================= CORE INTERACTIVE JOURNEY ================= -->
  <main class="w-full max-w-xl flex-grow flex items-center justify-center my-12 z-10">
    <div id="steps-container" class="relative w-full flex items-center justify-center min-h-[460px]">
      
      <!-- Step 1: The Grand Welcome -->
      <div id="step-1" class="glass-card w-full rounded-3xl p-8 md:p-12 flex flex-col items-center text-center gap-6 shadow-2xl">
        <div class="animate-stagger">
          <span class="inline-block text-6xl heart-beat cursor-default select-none">❤️</span>
        </div>
        <h1 class="font-serif-display text-4xl md:text-5xl font-bold text-gradient leading-tight animate-stagger">
          Hey Beautiful,
        </h1>
        <p class="text-stone-300 text-base md:text-lg leading-relaxed max-w-sm animate-stagger">
          I built a little world for you, just to bring a smile to your face on your special day.
        </p>
        <button onclick="goToStep(2)" class="gradient-btn animate-stagger py-3 px-8 text-white font-semibold rounded-full select-none mt-2">
          Let's Begin
        </button>
      </div>

      <!-- Step 2: The Core Message -->
      <div id="step-2" class="glass-card w-full rounded-3xl p-8 md:p-12 flex-col items-center text-center gap-6 shadow-2xl hidden opacity-0 translate-y-8 scale-95">
        <div class="animate-stagger">
          <span class="inline-block text-6xl filter drop-shadow-[0_0_15px_rgba(251,191,36,0.5)] select-none">🎉</span>
        </div>
        <h2 class="font-serif-display text-4xl md:text-5xl font-bold text-gradient leading-tight animate-stagger">
          Happy Birthday!
        </h2>
        <p class="text-stone-300 text-base md:text-lg leading-relaxed max-w-sm animate-stagger">
          Another year of you making the world brighter. Your existence is a gift, and I'm so lucky to witness it.
        </p>
        <button onclick="goToStep(3)" class="gradient-btn animate-stagger py-3 px-8 text-white font-semibold rounded-full select-none mt-2">
          There's more...
        </button>
      </div>

      <!-- Step 3: The Reasons Why (Bento Grid Layout) -->
      <div id="step-3" class="glass-card w-full rounded-3xl p-6 md:p-10 flex-col items-center text-center gap-6 shadow-2xl hidden opacity-0 translate-y-8 scale-95">
        <h2 class="font-serif-display text-3xl md:text-4xl font-bold text-gradient leading-tight animate-stagger">
          A Few Things I Adore About You
        </h2>
        
        <div class="grid grid-cols-1 md:grid-cols-2 gap-3 w-full text-left mt-2">
          <!-- Card 1 -->
          <div class="md:col-span-2 bg-white/5 border border-white/5 rounded-2xl p-5 hover:bg-white/10 transition-colors duration-300 animate-stagger">
            <h3 class="text-pink-300 font-bold text-base md:text-lg mb-1 flex items-center gap-2">✨ Your Unmatched Kindness</h3>
            <p class="text-stone-300 text-xs md:text-sm leading-relaxed">The genuine warmth you show to everyone is something truly rare and beautiful.</p>
          </div>
          <!-- Card 2 -->
          <div class="md:col-span-1 bg-white/5 border border-white/5 rounded-2xl p-5 hover:bg-white/10 transition-colors duration-300 animate-stagger">
            <h3 class="text-pink-300 font-bold text-base md:text-lg mb-1 flex items-center gap-2">😊 That Smile</h3>
            <p class="text-stone-300 text-xs md:text-sm leading-relaxed">It's a work of art.</p>
          </div>
          <!-- Card 3 -->
          <div class="md:col-span-2 bg-white/5 border border-white/5 rounded-2xl p-5 hover:bg-white/10 transition-colors duration-300 animate-stagger">
            <h3 class="text-pink-300 font-bold text-base md:text-lg mb-1 flex items-center gap-2">🌟 Your Radiant Spirit</h3>
            <p class="text-stone-300 text-xs md:text-sm leading-relaxed">Your passion for life is infectious. Being around you makes everything feel more exciting and possible.</p>
          </div>
        </div>

        <button onclick="goToStep(4)" class="gradient-btn animate-stagger py-3 px-8 text-white font-semibold rounded-full select-none mt-2">
          Remember this?
        </button>
      </div>

      <!-- Step 4: The Shared Memory -->
      <div id="step-4" class="glass-card w-full rounded-3xl p-8 md:p-12 flex-col items-center text-center gap-6 shadow-2xl hidden opacity-0 translate-y-8 scale-95">
        <h2 class="font-serif-display text-3xl md:text-4xl font-bold text-gradient leading-tight animate-stagger">
          That One Time...
        </h2>
        
        <!-- 3D Parallax Floating Polaroid -->
        <div class="perspective-container my-3 animate-stagger select-none">
          <div id="polaroid-card" class="polaroid bg-white p-3 pb-8 rounded shadow-[0_20px_40px_rgba(0,0,0,0.5)] transform -rotate-3 hover:rotate-0 transition-transform duration-300 flex flex-col items-center max-w-[210px] mx-auto border border-stone-200">
            <div class="w-full aspect-square bg-stone-100 overflow-hidden rounded relative border border-stone-200">
              <img src="https://i.ibb.co/6Z6XgCg/crush.webp" alt="Our favorite memory" class="w-full h-full object-cover select-none pointer-events-none">
            </div>
            <p class="font-serif-display text-stone-800 text-sm md:text-base italic mt-4 select-none">Our favorite memory.</p>
          </div>
        </div>

        <p class="text-stone-300 text-base md:text-lg leading-relaxed max-w-sm animate-stagger">
          Every moment with you feels like a scene from a movie I'd watch on repeat.
        </p>
        <button onclick="goToStep(5)" class="gradient-btn animate-stagger py-3 px-8 text-white font-semibold rounded-full select-none mt-2">
          One last thing...
        </button>
      </div>

      <!-- Step 5: The Birthday Wish & Finale -->
      <div id="step-5" class="glass-card w-full rounded-3xl p-8 md:p-12 flex-col items-center text-center gap-6 shadow-2xl hidden opacity-0 translate-y-8 scale-95">
        <div class="animate-stagger">
          <span class="inline-block text-6xl filter drop-shadow-[0_0_15px_rgba(244,63,94,0.4)] select-none">🎂</span>
        </div>
        <h2 class="font-serif-display text-3xl md:text-4xl font-bold text-gradient leading-tight animate-stagger">
          My Wish For You
        </h2>
        <p class="text-stone-300 text-base md:text-lg leading-relaxed max-w-sm animate-stagger">
          May the next year bring you all the love, success, and pure happiness you so rightfully deserve. May your dreams soar higher than ever.
        </p>
        
        <!-- Space Reserved for final message revealed later -->
        <div id="final-message-container" class="hidden h-0 overflow-hidden">
          <h1 id="final-text" class="font-serif-display text-3xl md:text-4xl font-extrabold bg-gradient-to-r from-pink-300 via-rose-300 to-rose-400 bg-clip-text text-transparent filter drop-shadow-[0_0_10px_rgba(244,63,94,0.4)] leading-tight mt-2 opacity-0 translate-y-4">
            Happy Birthday, my crush! ❤️
          </h1>
        </div>

        <button id="celebrate-btn" onclick="triggerCelebrateSequence()" class="gradient-btn animate-stagger py-3.5 px-10 text-white text-lg font-bold rounded-full select-none mt-2">
          Celebrate!
        </button>
      </div>

    </div>
  </main>


  <!-- ================= SUBTLE MODERN FOOTER ================= -->
  <footer class="text-stone-600 text-xs tracking-wider uppercase select-none z-10 py-4">
    Crafted especially for you
  </footer>


  <!-- ================= SYSTEM CODE & ANIMATION ENGINE ================= -->
  <script>
    let currentStep = 1;
    const maxSteps = 5;
    let isCelebrating = false;

    // --- SETUP THREE.JS 3D BACKGROUND ---
    const canvas = document.getElementById('canvas3d');
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 100);
    const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });

    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    renderer.setSize(window.innerWidth, window.innerHeight);
    camera.position.z = 12;

    // Lights
    const ambientLight = new THREE.AmbientLight(0xffffff, 0.6);
    scene.add(ambientLight);

    const dirLight = new THREE.DirectionalLight(0xffffff, 1.2);
    dirLight.position.set(5, 5, 10);
    scene.add(dirLight);

    const softPinkLight = new THREE.PointLight(0xff4d6d, 1.5, 30);
    softPinkLight.position.set(0, 0, 4);
    scene.add(softPinkLight);

    // Heart Shape Drawing Utility for 3D Geometry Extrusion
    const heartShape = new THREE.Shape();
    heartShape.moveTo(0, 0.5);
    heartShape.bezierCurveTo(0.5, 1.5, 2, 1.5, 2, 0.5);
    heartShape.bezierCurveTo(2, -0.5, 1, -1.5, 0, -2.5);
    heartShape.bezierCurveTo(-1, -1.5, -2, -0.5, -2, 0.5);
    heartShape.bezierCurveTo(-2, 1.5, -0.5, 1.5, 0, 0.5);

    const extrudeSettings = {
      depth: 0.3,
      bevelEnabled: true,
      bevelSegments: 4,
      steps: 1,
      bevelSize: 0.12,
      bevelThickness: 0.12
    };

    const heartGeometry = new THREE.ExtrudeGeometry(heartShape, extrudeSettings);
    heartGeometry.center();
    heartGeometry.scale(0.35, 0.35, 0.35); // Base scale normalization

    // Physical material to simulate light sheen reflection
    const heartMaterial = new THREE.MeshPhysicalMaterial({
      color: 0xff3b5c,
      roughness: 0.15,
      metalness: 0.12,
      clearcoat: 1.0,
      clearcoatRoughness: 0.1,
      transmission: 0.25,
      thickness: 0.4
    });

    const floatingHearts = [];
    const heartsCount = 23;

    for (let i = 0; i < heartsCount; i++) {
      const mesh = new THREE.Mesh(heartGeometry, heartMaterial);
      mesh.position.set(
        (Math.random() - 0.5) * 26,
        (Math.random() - 0.5) * 18,
        (Math.random() - 0.5) * 10 - 2
      );
      
      mesh.rotation.set(
        Math.random() * Math.PI,
        Math.random() * Math.PI,
        Math.random() * Math.PI
      );

      mesh.scale.setScalar(Math.random() * 0.4 + 0.35);

      mesh.userData = {
        speedY: Math.random() * 0.012 + 0.006,
        wiggleSpeed: Math.random() * 1.5 + 0.5,
        wiggleOffset: Math.random() * 10,
        wiggleScale: Math.random() * 0.3 + 0.1,
        initialX: mesh.position.x
      };

      scene.add(mesh);
      floatingHearts.push(mesh);
    }

    // Three.js Render Loop
    function updateFrame() {
      requestAnimationFrame(updateFrame);

      floatingHearts.forEach(mesh => {
        if (!isCelebrating) {
          // Standard Float drift motion
          mesh.position.y += mesh.userData.speedY;
          mesh.position.x = mesh.userData.initialX + Math.sin(Date.now() * 0.001 * mesh.userData.wiggleSpeed + mesh.userData.wiggleOffset) * mesh.userData.wiggleScale;
          
          mesh.rotation.y += 0.005;
          mesh.rotation.x += 0.002;

          // Recycle positions when drifting above screen space
          if (mesh.position.y > 10) {
            mesh.position.y = -10;
            mesh.position.x = (Math.random() - 0.5) * 26;
            mesh.userData.initialX = mesh.position.x;
          }
        } else {
          // Finale Sequence: Swirl outwards dynamically and lift off screen
          const directionFactor = mesh.position.x >= 0 ? 1 : -1;
          mesh.position.x += directionFactor * 0.22;
          mesh.position.y += 0.32;
          mesh.rotation.z += 0.08;
          mesh.scale.multiplyScalar(0.95); // shrink down to fade visually
        }
      });

      renderer.render(scene, camera);
    }

    updateFrame();

    // Responsive adjustment of Three.js Viewport limits
    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });


    // --- GUIDED STEPS SYSTEM & GSAP ---
    function goToStep(nextStepIndex) {
      if (nextStepIndex > maxSteps) return;

      const currentCard = document.getElementById(`step-${currentStep}`);
      const nextCard = document.getElementById(`step-${nextStepIndex}`);

      // Smoothly update visual Progress Bar track
      const progressPercent = (nextStepIndex / maxSteps) * 100;
      gsap.to("#progress-bar", { width: `${progressPercent}%`, duration: 0.5, ease: "power2.out" });

      const transitionTimeline = gsap.timeline({
        onStart: () => {
          nextCard.classList.remove('hidden');
          nextCard.classList.add('flex');
        },
        onComplete: () => {
          currentCard.classList.remove('flex');
          currentCard.classList.add('hidden');
          currentStep = nextStepIndex;
        }
      });

      // Outgoing card animation
      transitionTimeline.to(currentCard, {
        opacity: 0,
        y: -25,
        scale: 0.95,
        duration: 0.4,
        ease: "power2.inOut"
      });

      // Incoming card container presentation
      transitionTimeline.fromTo(nextCard,
        { opacity: 0, y: 25, scale: 0.95 },
        { opacity: 1, y: 0, scale: 1, duration: 0.5, ease: "power2.out" },
        "-=0.15"
      );

      // Stagger child elements of active container card
      const itemsToStagger = nextCard.querySelectorAll('.animate-stagger');
      if (itemsToStagger.length > 0) {
        transitionTimeline.fromTo(itemsToStagger,
          { opacity: 0, y: 15 },
          { opacity: 1, y: 0, duration: 0.45, stagger: 0.1, ease: "power2.out" },
          "-=0.35"
        );
      }
    }


    // --- POLAROID PARALLAX SYSTEM ---
    const polaroidContainer = document.getElementById('step-4');
    const polaroidCard = document.getElementById('polaroid-card');

    if (polaroidContainer && polaroidCard) {
      polaroidContainer.addEventListener('mousemove', (e) => {
        const bounds = polaroidCard.getBoundingClientRect();
        const cardCenterX = bounds.left + bounds.width / 2;
        const cardCenterY = bounds.top + bounds.height / 2;

        const deltaX = e.clientX - cardCenterX;
        const deltaY = e.clientY - cardCenterY;

        // Turn coordinates into limited 3D perspective rotation degree angles
        const rotateXDeg = -(deltaY / (bounds.height / 2)) * 14;
        const rotateYDeg = (deltaX / (bounds.width / 2)) * 14;

        gsap.to(polaroidCard, {
          rotateX: rotateXDeg,
          rotateY: rotateYDeg,
          scale: 1.05,
          duration: 0.4,
          ease: "power2.out",
          transformPerspective: 1000
        });
      });

      polaroidContainer.addEventListener('mouseleave', () => {
        gsap.to(polaroidCard, {
          rotateX: -3, // subtle base tilt return
          rotateY: 0,
          scale: 1,
          duration: 0.6,
          ease: "power2.out"
        });
      });
    }


    // --- CELEBRATE GRAND FINALE SEQUENCE ---
    function triggerCelebrateSequence() {
      const celebrateButton = document.getElementById('celebrate-btn');
      const finalContainer = document.getElementById('final-message-container');
      const finalText = document.getElementById('final-text');

      // 1. Disable and fade out the final step button
      gsap.to(celebrateButton, {
        opacity: 0,
        y: 15,
        duration: 0.45,
        ease: "power2.inOut",
        onComplete: () => {
          celebrateButton.style.display = "none";
          celebrateButton.setAttribute("disabled", "true");
        }
      });

      // 2. Reveal and slide/fade up the final surprise text message
      finalContainer.classList.remove('hidden');
      gsap.to(finalContainer, { height: "auto", duration: 0.4, ease: "power2.out" });
      gsap.fromTo(finalText,
        { opacity: 0, y: 25, scale: 0.9 },
        { opacity: 1, y: 0, scale: 1, duration: 1.1, ease: "elastic.out(1, 0.75)" }
      );

      // 3. Command Three.js hearts context update (swirling animation)
      isCelebrating = true;

      // 4. Initiate Multi-layered Confetti Explosion Sequence
      if (typeof confetti === "function") {
        const durationSec = 5 * 1000;
        const animationEndTime = Date.now() + durationSec;

        // Phase 1: Powerful bursts from screen corners instantly
        confetti({
          particleCount: 130,
          spread: 70,
          origin: { x: 0, y: 0.9 },
          angle: 55,
          colors: ['#f43f5e', '#ec4899', '#fdba74', '#ffffff']
        });
        confetti({
          particleCount: 130,
          spread: 70,
          origin: { x: 1, y: 0.9 },
          angle: 125,
          colors: ['#f43f5e', '#ec4899', '#fdba74', '#ffffff']
        });

        // Phase 2: Gentle, persistent shower of custom shape and emoji confetti
        const intervalTimer = setInterval(() => {
          const timeLeft = animationEndTime - Date.now();

          if (timeLeft <= 0) {
            return clearInterval(intervalTimer);
          }

          // Random standard colorful bursts along the screen plane
          confetti({
            particleCount: Math.floor(Math.random() * 3) + 2,
            spread: 60,
            origin: { x: Math.random(), y: Math.random() - 0.2 },
            colors: ['#ec4899', '#e11d48', '#fb7185', '#ffd1df']
          });

          // Special Emoji Heart confetti streams
          confetti({
            particleCount: 2,
            scalar: 2.2,
            shapes: ['emoji'],
            shapeOptions: {
              emoji: {
                value: ['❤️', '💖', '✨']
              }
            },
            origin: { x: Math.random(), y: Math.random() - 0.2 }
          });
        }, 180);
      }
    }
  </script>

