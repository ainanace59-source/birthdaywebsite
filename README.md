CTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy Birthday rumaizzz✨</title>
  
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
