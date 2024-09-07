
<script>
  import DarkMode from "$lib/DarkMode.svelte";
  import { onMount } from 'svelte';
  let position = 0;
  let scrollSpeed = 1.0;
  let images = [
    '/mobile/1.webp',
    '/mobile/2.webp',
    '/mobile/3.webp',
    '/mobile/4.webp',
    '/mobile/5.webp',
    '/mobile/6.webp'
  ];

  // On mount, clone the images for continuous scrolling
  /**
	 * @type {any[]}
	 */
  let clonedImages = [];

  onMount(() => {
    clonedImages = [...images, ...images]; // Clone images
    startScroll();
  });

  function startScroll() {
    function scroll() {
      position -= scrollSpeed;
      // @ts-ignore
      if (Math.abs(position) >= document.getElementById('carousel').scrollWidth / 2) {
        position = 0; // Reset position when half of the images have scrolled
      }
      requestAnimationFrame(scroll); // Continuously scroll
    }
    requestAnimationFrame(scroll);
  }

</script>

<nav class="bg-white dark:bg-gray-900 fixed w-full z-20 top-0 start-0 border-b border-gray-200 dark:border-gray-600">
  <div class=" flex flex-wrap items-center justify-between mx-auto p-4">
  <a href="/" class="flex items-center space-x-3 rtl:space-x-reverse">
      <img src="/AbonaLogo.webp" class="h-8" alt="Flowbite Logo">
      <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white"></span>
  </a>
  <div class="flex md:order-2 space-x-3 md:space-x-0 rtl:space-x-reverse">
      <DarkMode />
      <button data-collapse-toggle="navbar-sticky" type="button" class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600" aria-controls="navbar-sticky" aria-expanded="false">
        <span class="sr-only">Open main menu</span>
        <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 17 14">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 1h15M1 7h15M1 13h15"/>
        </svg>
    </button>
  </div>
  <div class="items-center justify-between hidden w-full md:flex md:w-auto md:order-1" id="navbar-sticky">
    <ul class="flex flex-col p-4 md:p-0 mt-4 font-medium border border-gray-100 rounded-lg bg-gray-50 md:space-x-8 rtl:space-x-reverse md:flex-row md:mt-0 md:border-0 md:bg-white dark:bg-gray-800 md:dark:bg-gray-900 dark:border-gray-700">
      <li>
        <a href="/" class="block py-2 px-3 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:hover:text-blue-700 md:p-0 md:dark:hover:text-blue-500 dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700" >Home</a>
      </li>
      <li>
        <a href="/" class="block py-2 px-3 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:hover:text-blue-700 md:p-0 md:dark:hover:text-blue-500 dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700">About</a>
      </li>
      <li>
        <a href="/" class="block py-2 px-3 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:hover:text-blue-700 md:p-0 md:dark:hover:text-blue-500 dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700">Services</a>
      </li>
      <li>
        <a href="/" class="block py-2 px-3 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:hover:text-blue-700 md:p-0 md:dark:hover:text-blue-500 dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700">Contact</a>
      </li>
    </ul>
  </div>
  </div>
</nav>

<!-- Body -->
<div class="container mx-auto px-5 md:pt-10">
  <!-- Hero -->
  <div class="flex flex-col-reverse lg:flex-row items-center space-y-4 md:space-y-0 md:space-x-8 p-4 lg:h-screen mt-14 lg:mt-0">
    <div class="w-full lg:w-1/2 justify-center items-center md:text-left">
      <h1 class="text-4xl xl:text-5xl font-bold my-6 text-center lg:text-start dark:text-white">App Title</h1>
      <p class="text-xl text-gray-600 text-center lg:text-start dark:text-slate-400">How it can help..</p>
      <div class="flex flex-col lg:flex-row space-y-8 lg:space-y-0 my-8">
        <a href="/" class="">
          <img class="w-1/2 md:w-1/3 lg:w-3/4 border rounded-lg mx-auto lg:mx-0" src="/google_store.png" alt="Google Play Store Button" />
        </a>
        <a href="/" class="">
          <img class="w-1/2 md:w-1/3 lg:w-3/4 rounded-lg border mx-auto lg:mx-0" src="/apple_store.png" alt="Google Play Store Button" />
        </a>
      </div>
    </div>
    <div class="w-full lg:w-1/2">
      <!-- Image -->
      <img class="h-auto rounded-lg w-3/4 mx-auto shadow-lg xl:w-1/2" src="/mobile/app.webp" alt="mobile app" />
      <!-- Video 
      <div class="aspect-video">
        <iframe class="w-full h-full" src="https://www.youtube.com/embed/zyNV17QEikM" title="YouTube video" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
      </div>
      -->
    </div>
  </div>
  <!-- Features -->
  <div class="mb-20">
    <h2 class="text-center text-3xl lg:text-4xl py-5 font-bold dark:text-white">Features</h2>
    <p class="mx-auto text-xl max-w-screen-lg text-gray-600 text-center dark:text-slate-400">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    <div class="py-10"></div>
    <div class="grid grid-cols-1 md:grid-cols-2 justify-items-center">
      <div class="bg-white dark:bg-slate-900 px-6 py-8">
        <div>
          <span class="inline-flex items-center justify-center p-2 bg-indigo-500 rounded-md shadow-lg">
            <svg class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path>
            </svg>
          </span>
        </div>
        <h3 class="text-slate-900 dark:text-white mt-5 text-lg font-medium tracking-tight">App Feature</h3>
        <p class="text-slate-500 dark:text-slate-400 mt-2 text-lg">
          Lorem ipsum dolor sit amet. Aut ipsa ducimus ea repellat consequatur est numquam Quis.
        </p>
      </div>
      <div class="bg-white dark:bg-slate-900 px-6 py-8">
        <div>
          <span class="inline-flex items-center justify-center p-2 bg-indigo-500 rounded-md shadow-lg">
            <svg class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 16.5V9.75m0 0l3 3m-3-3l-3 3M6.75 19.5a4.5 4.5 0 01-1.41-8.775 5.25 5.25 0 0110.233-2.33 3 3 0 013.758 3.848A3.752 3.752 0 0118 19.5H6.75z"></path>
            </svg>
          </span>
        </div>
        <h3 class="text-slate-900 dark:text-white mt-5 text-lg font-medium tracking-tight">App Feature</h3>
        <p class="text-slate-500 dark:text-slate-400 mt-2 text-lg">
          Lorem ipsum dolor sit amet. Aut ipsa ducimus ea repellat consequatur est numquam Quis.
        </p>
      </div>
      <div class="bg-white dark:bg-slate-900 px-6 py-8">
        <div>
          <span class="inline-flex items-center justify-center p-2 bg-indigo-500 rounded-md shadow-lg">
            <svg class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M16.5 10.5V6.75a4.5 4.5 0 10-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 002.25-2.25v-6.75a2.25 2.25 0 00-2.25-2.25H6.75a2.25 2.25 0 00-2.25 2.25v6.75a2.25 2.25 0 002.25 2.25z"></path>
            </svg>
          </span>
        </div>
        <h3 class="text-slate-900 dark:text-white mt-5 text-lg font-medium tracking-tight">App Feature</h3>
        <p class="text-slate-500 dark:text-slate-400 mt-2 text-lg">
          Lorem ipsum dolor sit amet. Aut ipsa ducimus ea repellat consequatur est numquam Quis.
        </p>
      </div>
      <div class="bg-white dark:bg-slate-900 px-6 py-8">
        <div>
          <span class="inline-flex items-center justify-center p-2 bg-indigo-500 rounded-md shadow-lg">
            <svg class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0l3.181 3.183a8.25 8.25 0 0013.803-3.7M4.031 9.865a8.25 8.25 0 0113.803-3.7l3.181 3.182m0-4.991v4.99"></path>
            </svg>
          </span>
        </div>
        <h3 class="text-slate-900 dark:text-white mt-5 text-lg font-medium tracking-tight">App Feature</h3>
        <p class="text-slate-500 dark:text-slate-400 mt-2 text-lg">
          Lorem ipsum dolor sit amet. Aut ipsa ducimus ea repellat consequatur est numquam Quis.
        </p>
      </div>
    </div>
  </div>
  <!-- Video
  <div class="aspect-video mb-20">
    <iframe class="w-full h-full" src="https://www.youtube.com/embed/zyNV17QEikM" title="YouTube video" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
  </div>
  -->
  <!-- Screenshots -->
  <div class="mb-20">
    <h2 class="text-center text-3xl lg:text-4xl py-5 font-bold dark:text-white">Screenshots</h2>
    <div class="py-10"></div>
    <div id="carousel-container" class="relative overflow-hidden max-w-screen-lg mx-auto">
      <div id="carousel" class="flex items-center w-max space-x-20" style="transform: translateX({position}px);">
        {#each clonedImages as img}
          <img src={img} alt="Screenshot" class="w-64 h-auto rounded-lg">
        {/each}
      </div>
    </div>
  </div>
</div>
