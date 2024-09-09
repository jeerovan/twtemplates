
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

  let currentIndex = 0;
  let testimonials = [
      {
        name: 'Kate',
        text: 'This app changed my life! Highly recommend it to everyone.',
        face: '/face/1.webp',
        company: 'Dotara'
      },
      {
        name: 'Julia',
        text: 'Absolutely fantastic service, really easy to use and very helpful.',
        face: '/face/3.webp',
        company: 'Galaxy'
      },
      {
        name: 'Celena',
        text: 'Great app for managing everything easily, 5 stars from me!',
        face: '/face/8.webp',
        company: 'Somalto'
      },
      {
        name: 'Ruby Williams',
        text: 'A must-have app for anyone looking for a simple and effective solution.',
        face: '/face/7.webp',
        company: 'Groot'
      }
    ];
    let swipeEffectClass = 'translate-x-full'; // Initial state for swipe effect

  onMount(() => {
    clonedImages = [...images, ...images]; // Clone images
    startScroll();

    // Set an interval to change the testimonials every 3 seconds
    const interval = setInterval(nextTestimonial, 3000);
    // Clean up the interval on component destroy
    return () => clearInterval(interval);
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

  // Function to handle swipe animation
  function nextTestimonial() {
    // Animate the current testimonial
    swipeEffectClass = '-translate-x-full opacity-0';
    setTimeout(() => {
      // Once the animation is over, switch to the next testimonial
      currentIndex = (currentIndex + 1) % testimonials.length;
      // Reset swipe effect class
      swipeEffectClass = 'translate-x-full';
      setTimeout(() => {
        swipeEffectClass = 'translate-x-0 opacity-100'; // Bring the next testimonial into view
      }, 10); // Small timeout to trigger the next animation
    }, 500); // Delay to match the transition duration
  }
  
  /**
	 * @type {number | null}
	 */
  let openIndex = null; // Track the currently open FAQ
  // Toggle the FAQ answer visibility
  /**
	 * @param {number} index
	 */
  function toggleFaq(index) {
    if (openIndex === index) {
      openIndex = null; // If the same FAQ is clicked again, close it
    } else {
      openIndex = index; // Open the clicked FAQ and close others
    }
  }

  let formData = { name : '', email : '', city : '', state : ''};
  let popupModal = false;
  let modalClass = "hidden";
  let modalTitle = "Title";
  // @ts-ignore
  let modalMessage = "Message";
  async function submitForm() {
    showModal("Form Submitted","We'll get back to you soon! Thank You.")
  }
  // @ts-ignore
  async function showModal(title,message){
    modalTitle = title;
    modalMessage = message;
    popupModal = true;
    modalClass = "";
  }
  async function closeModal(){
    popupModal = false;
    modalClass = "hidden";
  }

  let formPolicyAgreed = false;
  async function toggleFormPolicy(){
    formPolicyAgreed = !formPolicyAgreed;
  }

</script>

<svelte:head>
  <title>MyApp | Awesome You</title>
  <meta name="description" content="App landing page.">
  <meta name="author" content="Its Me">
</svelte:head>

<!-- Modal -->
<div class="{modalClass} fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50">
  <!-- Modal Content -->
  <div class="bg-white dark:bg-gray-800 dark:text-gray-300 rounded-lg shadow-lg w-full max-w-md">
    <!-- Header -->
    <div class="flex justify-between items-center p-4 border-b dark:border-gray-700">
      <h3 class="text-lg font-semibold">{modalTitle}</h3>
      <button on:click={closeModal} class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" class="w-6 h-6">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </div>
    
    <!-- Description -->
    <div class="p-4">
      <p class="text-gray-600 dark:text-gray-400">
        {modalMessage}
      </p>
    </div>
    
    <!-- Footer Button -->
    <div class="flex justify-end p-4 border-t dark:border-gray-700">
      <button on:click={closeModal} class="bg-primary-500 text-white px-4 py-2 rounded hover:bg-primary-600">
        Close
      </button>
    </div>
  </div>
</div>

<!-- Page -->
<nav class="bg-white dark:bg-gray-900 fixed w-full z-20 top-0 start-0 border-b border-gray-200 dark:border-gray-600">
  <div class=" flex flex-wrap items-center justify-between mx-auto p-4">
  <a href="/" class="flex items-center space-x-3">
      <img src="/my-app.webp" class="h-9 rounded-full" alt="Logo">
      <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white">MyApp</span>
  </a>
  <div class="flex md:order-2 space-x-3 md:space-x-0">
      <DarkMode />
      <button data-collapse-toggle="navbar-sticky" type="button" class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600" aria-controls="navbar-sticky" aria-expanded="false">
        <span class="sr-only">Open main menu</span>
        <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 17 14">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 1h15M1 7h15M1 13h15"/>
        </svg>
    </button>
  </div>
  <div class="items-center justify-between hidden w-full md:flex md:w-auto md:order-1" id="navbar-sticky">
    <ul class="flex flex-col p-4 md:p-0 mt-4 font-medium border border-gray-100 rounded-lg bg-gray-50 md:space-x-8 md:flex-row md:mt-0 md:border-0 md:bg-white dark:bg-gray-800 md:dark:bg-gray-900 dark:border-gray-700">
      <li>
        <a href="/" class="block py-2 px-3 text-primary-500 hover:text-primary-600 rounded hover:bg-gray-100 md:hover:bg-transparent md:p-0 dark:hover:bg-gray-700 md:dark:hover:bg-transparent dark:border-gray-700">Home</a>
      </li>
      <li>
        <a href="/" class="block py-2 px-3 text-primary-500 hover:text-primary-600 rounded hover:bg-gray-100 md:hover:bg-transparent md:p-0 dark:hover:bg-gray-700 md:dark:hover:bg-transparent dark:border-gray-700">About</a>
      </li>
      <li>
        <a href="/" class="block py-2 px-3 text-primary-500 hover:text-primary-600 rounded hover:bg-gray-100 md:hover:bg-transparent md:p-0 dark:hover:bg-gray-700 md:dark:hover:bg-transparent dark:border-gray-700">Services</a>
      </li>
      <li>
        <a href="/" class="block py-2 px-3 text-primary-500 hover:text-primary-600 rounded hover:bg-gray-100 md:hover:bg-transparent md:p-0 dark:hover:bg-gray-700 md:dark:hover:bg-transparent dark:border-gray-700">Contact</a>
      </li>
    </ul>
  </div>
  </div>
</nav>

<!-- Body -->
<div class="container mx-auto px-5 md:pt-10">
  <!-- Hero -->
  <div class="mb-32 md:mb-10 flex flex-col-reverse lg:flex-row items-center space-y-4 md:space-y-0 md:space-x-8 p-4 lg:h-screen mt-14 lg:mt-0">
    <div class="w-full lg:w-1/2 justify-center items-center md:text-left">
      <h1 class="text-4xl xl:text-5xl font-bold my-6 text-center lg:text-start dark:text-white">App Title</h1>
      <p class="text-xl text-gray-600 text-center lg:text-start dark:text-slate-400">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
      <div class="flex flex-col lg:flex-row space-y-8 lg:space-y-0 my-8">
        <a href="/" class="">
          <img class="w-1/2 md:w-1/3 lg:w-3/4 rounded-lg ring-1 ring-orange-900 hover:ring-orange-800 mx-auto lg:mx-0" src="/google_store.webp" alt="Google Play Store Button" />
        </a>
        <a href="/" class="">
          <img class="w-1/2 md:w-1/3 lg:w-3/4 rounded-lg ring-1 ring-orange-900 hover:ring-orange-800 mx-auto lg:mx-0" src="/apple_store.webp" alt="Google Play Store Button" />
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
  <div class="mb-32">
    <h2 class="text-center text-3xl lg:text-4xl py-5 font-bold dark:text-white">Features</h2>
    <p class="mx-auto text-xl max-w-screen-lg text-gray-600 text-center dark:text-slate-400">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    <div class="py-10"></div>
    <div class="grid grid-cols-1 md:grid-cols-2 justify-items-center max-w-screen-xl mx-auto bg-slate-50 dark:bg-slate-900 rounded-xl">
      <div class="px-6 py-8">
        <div>
          <span class="inline-flex items-center justify-center p-2 bg-primary-500 rounded-md shadow-lg">
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
      <div class="px-6 py-8">
        <div>
          <span class="inline-flex items-center justify-center p-2 bg-primary-500 rounded-md shadow-lg">
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
      <div class="px-6 py-8">
        <div>
          <span class="inline-flex items-center justify-center p-2 bg-primary-500 rounded-md shadow-lg">
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
      <div class="px-6 py-8">
        <div>
          <span class="inline-flex items-center justify-center p-2 bg-primary-500 rounded-md shadow-lg">
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
  <!-- Testimonials -->
  <div class="mb-64">
    <h2 class="text-center text-3xl lg:text-4xl py-5 font-bold dark:text-white">What our users say</h2>
    <div class="max-w-screen-md mx-auto relative p-6 h-64">
      <div class="absolute transition-transform duration-500 ease-in-out transform {swipeEffectClass} bg-slate-100 dark:bg-slate-900 p-10 rounded-xl">
        <div class="flex items-center">
          <svg class="w-4 h-4 text-red-600 ms-1" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 22 20">
              <path d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"/>
          </svg>
          <svg class="w-4 h-4 text-red-400 ms-1" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 22 20">
              <path d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"/>
          </svg>
          <svg class="w-4 h-4 text-orange-500 ms-1" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 22 20">
              <path d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"/>
          </svg>
          <svg class="w-4 h-4 text-green-400 ms-1" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 22 20">
              <path d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"/>
          </svg>
          <svg class="w-4 h-4 ms-1 text-green-600" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 22 20">
              <path d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"/>
          </svg>
        </div>
        <p class="text-xl font-medium my-10 dark:text-white">
          "{testimonials[currentIndex].text}"
        </p>
        <div class="flex flex-row space-x-6">
          <img class="rounded-full w-16 h16" src="{testimonials[currentIndex].face}" alt="person face" />
          <div class="">
            <p class="text-lg font-medium dark:text-white">{testimonials[currentIndex].name}</p>
            <p class="text-base font-medium dark:text-slate-400">CEO of {testimonials[currentIndex].company}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- Pricing -->
  <div class="mb-20">
    <h2 class="text-center text-3xl lg:text-4xl py-5 font-bold dark:text-white">Pricing Plans For All</h2>
    <p class="mx-auto text-xl max-w-screen-lg text-gray-600 text-center dark:text-slate-400">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
    <div class="py-8"></div>
    <div id="pricing" class="py-10 px-5 max-w-screen-xl mx-auto">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 justify-between">
        <div class="border rounded-2xl p-10 dark:border-slate-700">
          <h3 class="text-xl font-medium dark:text-white">Freelancer</h3>
          <p class=" mt-5 dark:text-slate-400">The essentials for your creativity.</p>
          <p class="mt-5 dark:text-slate-400">
            <span class="text-4xl dark:text-white">
              $25
            </span>/year
          </p>
          <div class="flex justify-center items-center md:justify-center space-x-4 py-8">
            <a href="/" class="w-full text-center px-4 py-2 rounded border border-slate-100 dark:text-white hover:border-slate-200 dark:border-slate-800 dark:hover:border-slate-700 bg-slate-50 dark:bg-slate-900">Buy Plan</a>
          </div>
          <ul>
            <li class="mb-5">
              <p class="flex items-center gap-4 text-sm dark:text-slate-400">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" class="fill-primary-500 w-5"><path fill-rule="evenodd" d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z" clip-rule="evenodd"></path></svg> 5 Users
              </p>
            </li>
            <li class="mb-5">
              <p class="flex items-center gap-4 text-sm dark:text-slate-400">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" class="fill-primary-500 w-5"><path fill-rule="evenodd" d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z" clip-rule="evenodd"></path></svg> Up to 1,000 subscribers
              </p>
            </li>
            <li class="mb-5">
              <p class="flex items-center gap-4 text-sm dark:text-slate-400">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" class="fill-primary-500 w-5"><path fill-rule="evenodd" d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z" clip-rule="evenodd"></path></svg> Basic support
              </p>
            </li>
          </ul>
        </div>
        <div class="border rounded-2xl p-10 dark:border-slate-700">
          <h3 class="text-xl font-medium dark:text-white">Startup</h3>
          <p class="mt-5 dark:text-slate-400">Lets fuel your engine.</p>
          <p class="mt-5 dark:text-slate-400">
            <span class="text-4xl dark:text-white">
              $50
            </span>/year
          </p>
          <div class="flex justify-center items-center md:justify-center space-x-4 py-8">
            <a href="/" class="w-full text-center px-4 py-2 rounded border border-slate-100 dark:text-white hover:border-slate-200 dark:border-slate-800 dark:hover:border-slate-700 bg-slate-50 dark:bg-slate-900">Buy Plan</a>
          </div>
          <ul>
            <li class="mb-5">
              <p class="flex items-center gap-4 text-sm dark:text-slate-400">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" class="fill-primary-500 w-5"><path fill-rule="evenodd" d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z" clip-rule="evenodd"></path></svg>50 Users
              </p>
            </li>
            <li class="mb-5">
              <p class="flex items-center gap-4 text-sm dark:text-slate-400">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" class="fill-primary-500 w-5"><path fill-rule="evenodd" d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z" clip-rule="evenodd"></path></svg> Up to 10,000 subscribers
              </p>
            </li>
            <li class="mb-5">
              <p class="flex items-center gap-4 text-sm dark:text-slate-400">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" class="fill-primary-500 w-5"><path fill-rule="evenodd" d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z" clip-rule="evenodd"></path></svg> Advanced support
              </p>
            </li>
          </ul>
        </div>
        <div class="border rounded-2xl p-10 dark:border-slate-700">
          <h3 class="text-xl font-medium dark:text-white">Enterprise</h3>
          <p class="mt-5 dark:text-slate-400">Pillars for your infrastructure</p>
          <p class="mt-5 dark:text-slate-400">
            <span class="text-4xl dark:text-white">
              $75
            </span>/year
          </p>
          <div class="flex justify-center items-center md:justify-center space-x-4 py-8">
            <a href="/" class="w-full text-center px-4 py-2 rounded border border-slate-100 dark:text-white hover:border-slate-200 dark:border-slate-800 dark:hover:border-slate-700 bg-slate-50 dark:bg-slate-900">Buy Plan</a>
          </div>
          <ul>
            <li class="mb-5">
              <p class="flex items-center gap-4 text-sm dark:text-slate-400">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" class="fill-primary-500 w-5"><path fill-rule="evenodd" d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z" clip-rule="evenodd"></path></svg> Unlimited users
              </p>
            </li>
            <li class="mb-5">
              <p class="flex items-center gap-4 text-sm dark:text-slate-400">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" class="fill-primary-500 w-5"><path fill-rule="evenodd" d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z" clip-rule="evenodd"></path></svg> Unlimited subscribers
              </p>
            </li>
            <li class="mb-5">
              <p class="flex items-center gap-4 text-sm dark:text-slate-400">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" class="fill-primary-500 w-5"><path fill-rule="evenodd" d="M16.704 4.153a.75.75 0 01.143 1.052l-8 10.5a.75.75 0 01-1.127.075l-4.5-4.5a.75.75 0 011.06-1.06l3.894 3.893 7.48-9.817a.75.75 0 011.05-.143z" clip-rule="evenodd"></path></svg> Advanced support
              </p>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
  <!-- FAQs -->
  <div class="mb-32">
    <h2 class="text-center text-3xl lg:text-4xl py-5 font-bold dark:text-white">FAQs</h2>
    <div class="py-8"></div>
    <div class="max-w-screen-xl mx-auto px-5" role="tablist">
      <button type="button" class="w-full text-start" on:click={() => toggleFaq(1)} role="tab" tabindex="0" aria-expanded={openIndex === 1}
        aria-controls="accordion-collapse-body-{openIndex}" aria-selected={openIndex === 1} data-accordion-target="#accordion-collapse-body-{openIndex}" >
        <div class="flex items-center justify-between w-full p-5 font-medium text-gray-500 border border-b-0 border-gray-200 rounded-t-xl dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800 gap-3">
          <h3>What is your app?</h3>
          <svg data-accordion-icon class="transition-transform duration-300 w-3 h-3 {openIndex === 1 ? '' : 'rotate-180'} shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5 5 1 1 5"/>
          </svg>
        </div>
        <div class="{`${openIndex === 1 ? '' : 'hidden'}`}">
          <div class="p-5 border border-b-0 border-gray-200 dark:border-gray-700 bg-slate-50 dark:bg-gray-900">
            <p class="mb-2 text-gray-500 dark:text-gray-400">Your app is awesome.</p>
            <p class="text-gray-500 dark:text-gray-400">Check out this guide to <a href="/" class="text-blue-600 dark:text-blue-500 hover:underline">get started</a> and start using it.</p>
          </div>
        </div>
      </button>
      <button type="button" class="w-full text-start" on:click={() => toggleFaq(2)} role="tab" tabindex="0" aria-expanded={openIndex === 2}
        aria-controls="accordion-collapse-body-{openIndex}" aria-selected={openIndex === 2} data-accordion-target="#accordion-collapse-body-{openIndex}">
        <div class="flex items-center justify-between w-full p-5 font-medium text-gray-500 border border-b-0 border-gray-200 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800 gap-3">
          <h3>Is there a Figma file available?</h3>
          <svg data-accordion-icon class="transition-transform duration-300 w-3 h-3 {openIndex === 2 ? '' : 'rotate-180'} shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5 5 1 1 5"/>
          </svg>
        </div>
        <div class={`${openIndex === 2 ? '' : 'hidden'}`}>
          <div class="p-5 border border-b-0 border-gray-200 dark:border-gray-700 bg-slate-50 dark:bg-gray-900">
            <p class="mb-2 text-gray-500 dark:text-gray-400">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. </p>
            <p class="text-gray-500 dark:text-gray-400">Check out the <a href="/" class="text-blue-600 dark:text-blue-500 hover:underline">Figma design system</a> based on lorem ipsum guide.</p>
          </div>
        </div>
      </button>
      <button type="button" class="w-full text-start" on:click={() => toggleFaq(3)} role="tab" tabindex="0" aria-expanded={openIndex === 3}
        aria-controls="accordion-collapse-body-{openIndex}" aria-selected={openIndex === 3} data-accordion-target="#accordion-collapse-body-{openIndex}">
        <div class="flex items-center justify-between w-full p-5 font-medium text-gray-500 border border-b-0 border-gray-200 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800 gap-3">
          <h3>How to use your app?</h3>
          <svg data-accordion-icon class="transition-transform duration-300 w-3 h-3 {openIndex === 3 ? '' : 'rotate-180'} shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5 5 1 1 5"/>
          </svg>
        </div>
        <div class={`${openIndex === 3 ? '' : 'hidden'}`}>
          <div class="p-5 border border-b-0 border-gray-200 dark:border-gray-700 bg-slate-50 dark:bg-gray-900">
            <p class="mb-2 text-gray-500 dark:text-gray-400">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
            <p class="mb-2 text-gray-500 dark:text-gray-400">Learn more about these features:</p>
            <ul class="ps-5 text-gray-500 list-disc dark:text-gray-400">
              <li><a href="/" class="text-blue-600 dark:text-blue-500 hover:underline">Go magical</a></li>
              <li><a href="/" rel="nofollow" class="text-blue-600 dark:text-blue-500 hover:underline">Onboarding</a></li>
            </ul>
          </div>
        </div>
      </button>
      <button type="button" class="w-full text-start" on:click={() => toggleFaq(4)} role="tab" tabindex="0" aria-expanded={openIndex === 4}
        aria-controls="accordion-collapse-body-{openIndex}" aria-selected={openIndex === 4} data-accordion-target="#accordion-collapse-body-{openIndex}">
        <div class="flex items-center justify-between w-full p-5 font-medium text-gray-500 border border-gray-200 dark:border-gray-700 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800 gap-3">
          <h3>Do you have a free plan?</h3>
          <svg data-accordion-icon class="transition-transform duration-300 w-3 h-3 {openIndex === 4 ? '' : 'rotate-180'} shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5 5 1 1 5"/>
          </svg>
        </div>
        <div class={`${openIndex === 4 ? '' : 'hidden'}`}>
          <div class="p-5 border border-t-0 border-gray-200 dark:border-gray-700 bg-slate-50 dark:bg-gray-900">
            <p class="mb-2 text-gray-500 dark:text-gray-400">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
            <p class="mb-2 text-gray-500 dark:text-gray-400">check out the plans in pricing section.</p>
          </div>
        </div>
      </button>
    </div>
  </div>
  <!-- Contact-->
  <div class="mb-32">
    <h2 class="text-center text-3xl lg:text-4xl py-5 font-bold dark:text-white">Contact</h2>
    <div class="py-8"></div>
    <div class="max-w-screen-xl mx-auto px-5">
      <div class="mx-auto w-full lg:w-1/2 border rounded-lg py-10 px-5 dark:border-slate-700">
        <form method="post" on:submit|preventDefault={submitForm}>
          <div class="mb-6">
            <label for="default-input" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Name</label>
            <input id="name" placeholder="Name" bind:value={formData.name} class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white"/>
          </div>
          <div class="mb-6">
            <label for="default-input" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Email</label>
            <input id="email" placeholder="Email" bind:value={formData.email} required class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white"/>
          </div>
          <div class="grid grid-cols-1 md:grid-cols-2 md:gap-5">
            <div class="mb-6">
              <label for="default-input" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">City</label>
              <input id="city" placeholder="City" bind:value={formData.city} class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white"/>
            </div>
            <div class="mb-">
              <label for="default-input" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">State</label>
              <input id="state" placeholder="State" bind:value={formData.state} class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white "/>
            </div>
          </div>
          <div class="flex gap-x-4 sm:col-span-2">
            <div class="flex h-6 items-center">
              <button type="button" class="flex w-8 flex-none cursor-pointer rounded-full {formPolicyAgreed ? 'bg-primary-600' : 'bg-gray-200'} p-px ring-1 ring-inset ring-gray-900/5 transition-colors duration-200 ease-in-out focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600" role="switch" aria-checked="false" aria-labelledby="switch-1-label" on:click={toggleFormPolicy}>
                <span class="sr-only">Agree to policies</span>
                <!-- Enabled: "translate-x-3.5", Not Enabled: "translate-x-0" -->
                <span aria-hidden="true" class="h-4 w-4 {formPolicyAgreed ? 'translate-x-3.5' : 'translate-x-0'} transform rounded-full bg-white shadow-sm ring-1 ring-gray-900/5 transition duration-200 ease-in-out"></span>
              </button>
            </div>
            <label for="default-input" class="text-sm leading-6 text-gray-600" id="switch-1-label">
              By selecting this, you agree to our
              <a href="/" class="font-semibold text-blue-500">privacy&nbsp;policy</a>.
            </label>
          </div>
          <div class="py-6"></div>
          <button type="submit" class="w-full text-center px-4 py-2 rounded border border-slate-100 dark:text-white hover:border-slate-200 dark:border-slate-800 dark:hover:border-slate-700 bg-slate-50 dark:bg-slate-900">Submit</button>
        </form>
      </div>
    </div>
  </div>
</div>  
  
<!-- Footer -->
<footer class="bg-white dark:bg-gray-900 p-6">
  <div class="mx-auto w-full p-6 py-6 lg:py-8">
      <div class="md:flex md:justify-between">
        <div class="mb-6 md:mb-0">
            <a href="/" class="flex items-center justify-center">
                <img src="/my-app.webp" class="h-9 me-3 rounded-full" alt="Logo" />
                <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white">MyApp</span>
            </a>
        </div>
        <div class="grid grid-cols-2 gap-8 sm:gap-6 sm:grid-cols-3">
            <div>
                <h2 class="mb-6 text-sm font-semibold text-gray-900 uppercase dark:text-white">Resources</h2>
                <ul class="text-gray-500 dark:text-gray-400 font-medium">
                    <li class="mb-4">
                        <a href="/" class="hover:underline">Docs</a>
                    </li>
                    <li>
                        <a href="/" class="hover:underline">Blog</a>
                    </li>
                </ul>
            </div>
            <div>
                <h2 class="mb-6 text-sm font-semibold text-gray-900 uppercase dark:text-white">Follow us</h2>
                <ul class="text-gray-500 dark:text-gray-400 font-medium">
                    <li class="mb-4">
                        <a href="/" class="hover:underline ">Github</a>
                    </li>
                    <li>
                        <a href="/" class="hover:underline">Discord</a>
                    </li>
                </ul>
            </div>
            <div>
                <h2 class="mb-6 text-sm font-semibold text-gray-900 uppercase dark:text-white">Legal</h2>
                <ul class="text-gray-500 dark:text-gray-400 font-medium">
                    <li class="mb-4">
                        <a href="/" class="hover:underline">Privacy Policy</a>
                    </li>
                    <li>
                        <a href="/" class="hover:underline">Terms &amp; Conditions</a>
                    </li>
                </ul>
            </div>
        </div>
    </div>
    <hr class="my-6 border-gray-200 sm:mx-auto dark:border-gray-700 lg:my-8" />
    <div class="sm:flex sm:items-center sm:justify-between">
        <span class="text-sm text-gray-500 sm:text-center dark:text-gray-400">© {new Date().getFullYear()} <a href="/" class="hover:underline">MyApp™</a>. All Rights Reserved.
        </span>
        <div class="flex mt-4 sm:justify-center sm:mt-0">
            <a href="/" class="text-gray-500 hover:text-gray-900 dark:hover:text-white">
                <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 8 19">
                      <path fill-rule="evenodd" d="M6.135 3H8V0H6.135a4.147 4.147 0 0 0-4.142 4.142V6H0v3h2v9.938h3V9h2.021l.592-3H5V3.591A.6.6 0 0 1 5.592 3h.543Z" clip-rule="evenodd"/>
                  </svg>
                <span class="sr-only">Facebook page</span>
            </a>
            <a href="/" class="text-gray-500 hover:text-gray-900 dark:hover:text-white ms-5">
                <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 21 16">
                      <path d="M16.942 1.556a16.3 16.3 0 0 0-4.126-1.3 12.04 12.04 0 0 0-.529 1.1 15.175 15.175 0 0 0-4.573 0 11.585 11.585 0 0 0-.535-1.1 16.274 16.274 0 0 0-4.129 1.3A17.392 17.392 0 0 0 .182 13.218a15.785 15.785 0 0 0 4.963 2.521c.41-.564.773-1.16 1.084-1.785a10.63 10.63 0 0 1-1.706-.83c.143-.106.283-.217.418-.33a11.664 11.664 0 0 0 10.118 0c.137.113.277.224.418.33-.544.328-1.116.606-1.71.832a12.52 12.52 0 0 0 1.084 1.785 16.46 16.46 0 0 0 5.064-2.595 17.286 17.286 0 0 0-2.973-11.59ZM6.678 10.813a1.941 1.941 0 0 1-1.8-2.045 1.93 1.93 0 0 1 1.8-2.047 1.919 1.919 0 0 1 1.8 2.047 1.93 1.93 0 0 1-1.8 2.045Zm6.644 0a1.94 1.94 0 0 1-1.8-2.045 1.93 1.93 0 0 1 1.8-2.047 1.918 1.918 0 0 1 1.8 2.047 1.93 1.93 0 0 1-1.8 2.045Z"/>
                  </svg>
                <span class="sr-only">Discord community</span>
            </a>
            <a href="/" class="text-gray-500 hover:text-gray-900 dark:hover:text-white ms-5">
                <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 20 17">
                  <path fill-rule="evenodd" d="M20 1.892a8.178 8.178 0 0 1-2.355.635 4.074 4.074 0 0 0 1.8-2.235 8.344 8.344 0 0 1-2.605.98A4.13 4.13 0 0 0 13.85 0a4.068 4.068 0 0 0-4.1 4.038 4 4 0 0 0 .105.919A11.705 11.705 0 0 1 1.4.734a4.006 4.006 0 0 0 1.268 5.392 4.165 4.165 0 0 1-1.859-.5v.05A4.057 4.057 0 0 0 4.1 9.635a4.19 4.19 0 0 1-1.856.07 4.108 4.108 0 0 0 3.831 2.807A8.36 8.36 0 0 1 0 14.184 11.732 11.732 0 0 0 6.291 16 11.502 11.502 0 0 0 17.964 4.5c0-.177 0-.35-.012-.523A8.143 8.143 0 0 0 20 1.892Z" clip-rule="evenodd"/>
              </svg>
                <span class="sr-only">Twitter page</span>
            </a>
            <a href="/" class="text-gray-500 hover:text-gray-900 dark:hover:text-white ms-5">
                <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 20 20">
                      <path fill-rule="evenodd" d="M10 .333A9.911 9.911 0 0 0 6.866 19.65c.5.092.678-.215.678-.477 0-.237-.01-1.017-.014-1.845-2.757.6-3.338-1.169-3.338-1.169a2.627 2.627 0 0 0-1.1-1.451c-.9-.615.07-.6.07-.6a2.084 2.084 0 0 1 1.518 1.021 2.11 2.11 0 0 0 2.884.823c.044-.503.268-.973.63-1.325-2.2-.25-4.516-1.1-4.516-4.9A3.832 3.832 0 0 1 4.7 7.068a3.56 3.56 0 0 1 .095-2.623s.832-.266 2.726 1.016a9.409 9.409 0 0 1 4.962 0c1.89-1.282 2.717-1.016 2.717-1.016.366.83.402 1.768.1 2.623a3.827 3.827 0 0 1 1.02 2.659c0 3.807-2.319 4.644-4.525 4.889a2.366 2.366 0 0 1 .673 1.834c0 1.326-.012 2.394-.012 2.72 0 .263.18.572.681.475A9.911 9.911 0 0 0 10 .333Z" clip-rule="evenodd"/>
                </svg>
                <span class="sr-only">GitHub account</span>
            </a>
            <a href="/" class="text-gray-500 hover:text-gray-900 dark:hover:text-white ms-5">
                <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 0a10 10 0 1 0 10 10A10.009 10.009 0 0 0 10 0Zm6.613 4.614a8.523 8.523 0 0 1 1.93 5.32 20.094 20.094 0 0 0-5.949-.274c-.059-.149-.122-.292-.184-.441a23.879 23.879 0 0 0-.566-1.239 11.41 11.41 0 0 0 4.769-3.366ZM8 1.707a8.821 8.821 0 0 1 2-.238 8.5 8.5 0 0 1 5.664 2.152 9.608 9.608 0 0 1-4.476 3.087A45.758 45.758 0 0 0 8 1.707ZM1.642 8.262a8.57 8.57 0 0 1 4.73-5.981A53.998 53.998 0 0 1 9.54 7.222a32.078 32.078 0 0 1-7.9 1.04h.002Zm2.01 7.46a8.51 8.51 0 0 1-2.2-5.707v-.262a31.64 31.64 0 0 0 8.777-1.219c.243.477.477.964.692 1.449-.114.032-.227.067-.336.1a13.569 13.569 0 0 0-6.942 5.636l.009.003ZM10 18.556a8.508 8.508 0 0 1-5.243-1.8 11.717 11.717 0 0 1 6.7-5.332.509.509 0 0 1 .055-.02 35.65 35.65 0 0 1 1.819 6.476 8.476 8.476 0 0 1-3.331.676Zm4.772-1.462A37.232 37.232 0 0 0 13.113 11a12.513 12.513 0 0 1 5.321.364 8.56 8.56 0 0 1-3.66 5.73h-.002Z" clip-rule="evenodd"/>
              </svg>
                <span class="sr-only">Dribbble account</span>
            </a>
        </div>
    </div>
  </div>
</footer>
