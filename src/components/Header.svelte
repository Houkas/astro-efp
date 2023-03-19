<script>
  import { fade } from "svelte/transition";
  import { onMount, onDestroy } from "svelte";

  let isAnimatedBarVisible = true;
  let isDeviceMobile = false;
  let url = "";
  let isMenuOpen = false;
  $: y = 0;
  $: deviceWidth = 0;
  $: deviceHeight = 0;
  $: isHomePage = url == "/" ? true : false;


  onMount(() => {
    url = window.location.pathname;
    if (deviceWidth < 640) {
      isDeviceMobile = true;
    }
  });

  onDestroy(() => (isAnimatedBarVisible = true));

  setTimeout(function () {
    isAnimatedBarVisible = false;
  }, 1500);

  function openMobileMenu() {
    isMenuOpen = !isMenuOpen;
  }

</script>

<svelte:window
  bind:scrollY={y}
  bind:innerHeight={deviceHeight}
  bind:innerWidth={deviceWidth}
/>
<nav>
  <div
    class=" z-50 w-full px-2 sm:px-4 py-2.5 fixed {y == 0 && isHomePage
      ? 'bg-transparent duration-500'
      : 'bg-[#F8FBFB] duration-500'}"
  >
    <div class="container flex flex-wrap justify-between items-center">
      <a href="/">
        <img
          src="/logo-efp-with-initials.png"
          class="logo-efp"
          alt="efp logo"
        />
      </a>

      <button
        data-collapse-toggle="mobile-menu"
        type="button"
        class="inline-flex items-center p-2 ml-3 text-sm text-gray-500 rounded-lg md:hidden focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 "
        aria-controls="mobile-menu"
        aria-expanded="false"
        on:click={openMobileMenu}
      >
        <span class="sr-only">Open main menu</span>
        <svg
          class="w-6 h-6"
          fill="currentColor"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
          ><path
            fill-rule="evenodd"
            d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
            clip-rule="evenodd"
          /></svg
        >
        <svg
          class="hidden w-6 h-6"
          fill="currentColor"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
          ><path
            fill-rule="evenodd"
            d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
            clip-rule="evenodd"
          /></svg
        >
      </button>
      {#if deviceWidth > 640}
        <div class="w-full md:block md:w-auto" id="mobile-menu">
          <ul
            class="flex flex-col mt-4 md:flex-row md:space-x-8 md:mt-0 md:text-sm md:font-medium"
          >
            <li transition:fade class={isHomePage === true ? "hidden" : ""}>
              <a href="/" class="block py-2 pr-4 pl-3 md:p-0">Accueil</a>
            </li>
            <li>
              <a href="/realisations" class="block py-2 pr-4 pl-3 md:p-0"
                >Réalisations</a
              >
            </li>
            <!--<li>
              <a href="/partenaires" class="block py-2 pr-4 pl-3 md:p-0"
                >Partenaires</a
              >
            </li>-->
            <li>
              <a href="/articles" class="block py-2 pr-4 pl-3 md:p-0"
                >Articles</a
              >
            </li>
            <li>
              <a href="/contact" class="block py-2 pr-4 pl-3 md:p-0">Contact</a>
            </li>
          </ul>
        </div>
      {/if}
    </div>
  </div>
  {#if isDeviceMobile === true && isMenuOpen === true}
    <div
      transition:fade
      class="z-[49] fixed bg-[#F8FBFB] w-screen h-screen py-[70px]"
    >
      <div
        class="flex flex-row justify-center w-full h-full md:block md:w-auto"
        id="mobile-menu"
      >
        <div
          class="bg-degrade absolute  w-1/2 lg:w-1/4 h-[98%] lg:h-[90%] slide-tb {isAnimatedBarVisible === true
            ? 'z-[9]'
            : 'z-0'}"
          id="animated-bar"
        />

        <ul
          class="h-full flex flex-col items-center justify-center mt-4 md:flex-row md:space-x-8 md:mt-0 md:text-sm md:font-medium"
        >
          <li
            transition:fade
            class="py-6 {isHomePage === true ? 'hidden' : ''}"
          >
            <a href="/" class="block py-2 pr-4 pl-3 md:p-0 text-center "
              >Accueil</a
            >
          </li>
          <li class="py-6">
            <a
              href="/realisations"
              class="block py-2 pr-4 pl-3 md:p-0 text-center ">Réalisations</a
            >
          </li>
          <!--<li class="py-6">
            <a
              href="/partenaires"
              class="block py-2 pr-4 pl-3 md:p-0 text-center ">Partenaires</a
            >
          </li>-->
          <li class="py-6">
            <a href="/articles" class="block py-2 pr-4 pl-3 md:p-0 text-center "
              >Articles</a
            >
          </li>
          <li class="py-6">
            <a href="/contact" class="block py-2 pr-4 pl-3 md:p-0">Contact</a>
          </li>
        </ul>
      </div>
    </div>
  {/if}
</nav>

<style lang="scss">
  .bg-degrade {
    background: linear-gradient(180deg, #7dfeff 0%, #e0f8bc 100%);
  }
  @keyframes slidein {
    from {
      margin-left: -10px;
    }
    to {
      margin-left: 0;
    }
  }
  nav {
    min-width: 100%;
    z-index: 25;
  }
  .slide-tb {
    opacity: 0;
    animation-name: SlideTb;
    animation-iteration-count: 1;
    animation-timing-function: ease-in-out;
    animation-duration: 0.75s;
  }
  @keyframes SlideTb {
    0% {
      opacity: 1;
      height: 0;
    }
    50% {
      height: 100vh;
    }
    100% {
      opacity: 1;
      height: 0;
    }
  }
  .fade-in {
    opacity: 1;
    animation-name: fadeInOpacity;
    animation-iteration-count: 1;
    animation-timing-function: ease-in;
    animation-duration: 2s;
  }
  @keyframes fadeInOpacity {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
  .fade-out {
    opacity: 1;
    animation-name: fadeOutOpacity;
    animation-iteration-count: 1;
    animation-timing-function: ease-out;
    animation-duration: 2s;
  }
  @keyframes fadeOutOpacity {
    0% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }
  .container {
    max-width: inherit !important;
    .logo-efp {
      width: 50px;
      height: 50px;
    }
  }
  #mobile-menu ul li {
    a {
      text-transform: uppercase;
      font-family: "Zen Kaku Gothic New", sans-serif;
      font-size: 0.85em;
      font-weight: 800;
      transition: all 0.25s ease-out;
      transform: skewX(0deg);
      color: #122023;
    }
    a::before {
      display: block;
      position: absolute;
      z-index: -10;
      left: -15px;
      opacity: 1;
      content: "";
      background-image: url("/circle_degrade.svg");
      height: 20px;
      width: 20px;
      -webkit-transition: all cubic-bezier(0.55, 0.085, 0.68, 0.53) s;
      transition: all 0.25s linear;
      opacity: 0;
      transform: skewX(10deg);
    }
    a:hover::before {
      opacity: 1;
      transition: all 0.25s linear;
      animation-duration: 0.25s;
      animation-name: slidein;
    }
    a:hover {
      transform: skewX(-10deg);
      color: #004e63;
    }
  }
  @media (max-width: 768px) {
    #mobile-menu ul li {
      a {
        font-size: 2em;
        font-weight: 800;
      }
    }
  }
</style>
