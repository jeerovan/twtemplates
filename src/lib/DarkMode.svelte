<!-- src/lib/DarkMode.svelte -->
<script>
  import { onMount } from 'svelte';
  let darkMode = false;
  let darkState = "";
  let lightState = "";
  // Initialize based on the user's previous preference or system setting
  onMount(() => {
    darkMode = localStorage.getItem('theme') === 'dark' || 
               (!localStorage.getItem('theme') && window.matchMedia('(prefers-color-scheme: dark)').matches);
    applyTheme();
  });

  // Function to toggle and store dark mode preference
  function toggleDarkMode() {
    darkMode = !darkMode;
    applyTheme();
  }

  // Function to apply the correct theme
  function applyTheme() {
    if (darkMode) {
      document.documentElement.classList.add('dark');
      localStorage.setItem('theme', 'dark');
    } else {
      document.documentElement.classList.remove('dark');
      localStorage.setItem('theme', 'light');
    }
    darkState = darkMode ? "hidden" : "";
    lightState = darkMode ? "" : "hidden";
  }
  
</script>

<button id="theme-toggle" on:click={toggleDarkMode} aria-label="toggle dark mode" type="button" class="w-10 h-10 text-gray-500 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700 rounded-full text-sm p-2.5 hover:text-primary-500 dark:hover:text-primary-500 transition-all hover:-rotate-90 duration-500 relative">
  <svg id="theme-toggle-dark-icon" class="absolute top-2.5 left-2.5 {darkState} w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z"></path></svg>
  <svg id="theme-toggle-light-icon" class="absolute top-2.5 left-2.5 {lightState} w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z" fill-rule="evenodd" clip-rule="evenodd"></path></svg>
</button>
