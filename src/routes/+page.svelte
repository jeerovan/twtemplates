
<script>
  import DarkMode from "$lib/DarkMode.svelte";
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
      <h1 class="text-4xl xl:text-5xl font-bold my-6 text-center lg:text-start">App Title</h1>
      <p class="text-lg text-gray-600 text-center lg:text-start">How it can help..</p>
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
      <img class="h-auto rounded-lg w-3/4 mx-auto shadow-lg 2xl:w-1/2" src="/mobile_app.jpg" alt="mobile app" />
      <!-- Video 
      <div class="aspect-video">
        <iframe class="w-full h-full" src="https://www.youtube.com/embed/zyNV17QEikM" title="YouTube video" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
      </div>
      -->
    </div>
  </div>
  <!-- Features -->
   <div>
    <h1 class="text-center text-3xl lg:text-4xl py-10">Features</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3">
      <div class="bg-white dark:bg-slate-900 px-6 py-8 ring-1 ring-slate-900/5">
        <div>
          <span class="inline-flex items-center justify-center p-2 bg-indigo-500 rounded-md shadow-lg">
            <svg class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path>
            </svg>
          </span>
        </div>
        <h3 class="text-slate-900 dark:text-white mt-5 text-base font-medium tracking-tight">App Feature One</h3>
        <p class="text-slate-500 dark:text-slate-400 mt-2 text-sm">
          Lorem ipsum dolor sit amet. Aut ipsa ducimus ea repellat consequatur est numquam Quis.
        </p>
      </div>
      
    </div>
   </div>
</div>
