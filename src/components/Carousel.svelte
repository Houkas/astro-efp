<script lang="ts">
  ////import { apiRealisationsData } from "../../shared/store";
  import type { Realisation } from "../types/realisation";
  import { fade, slide } from "svelte/transition";
  //import { urlStrapiEfpDEV } from "../../shared/config";
  let firstRel: Realisation = {
    attributes: {
      title: "test",
      createdAt:"test",
      meta_description:"test",
      images:"test",
      body: "test",
      slug: "test",
      miniature: {
        data: {
          attributes: { url: "/depot-efp.jpg" },
        },
      },
    },
  };
  let secondtRel: Realisation = {
    attributes: {
      title: "test",
      createdAt:"test",
      meta_description:"test",
      images:"test",
      body: "test",
      slug: "test",
      miniature: {
        data: {
          attributes: { url: "/depot-efp.jpg" },
        },
      },
    },
  };
  let thirdRel: Realisation = {
    attributes: {
      title: "test",
      createdAt:"test",
      meta_description:"test",
      images:"test",
      body: "test",
      slug: "test",
      miniature: {
        data: {
          attributes: { url: "/depot-efp.jpg" },
        },
      },
    },
  };

  let realisations: Realisation[] = [firstRel, secondtRel, thirdRel];

  /*apiRealisationsData.subscribe((values) => {
      realisations = values;
    });*/

  let lastRealImg: string[] = [];

  realisations = realisations.sort(
    (a, b) =>
      Date.parse(b.attributes.createdAt) - Date.parse(a.attributes.createdAt)
  );
  realisations = realisations.slice(0, 3);

  realisations.forEach((realisaion) => {
    lastRealImg.push(realisaion.attributes.miniature.data.attributes.url);
  });

  let index = 0;

  const interval = setInterval(function () {
    //next();
  }, 4000);

  const next = () => {
    index = (index + 1) % lastRealImg.length;
  };
  const prev = () => {
    index = index != 0 ? index - 1 : index + lastRealImg.length - 1;
  };

  const btnNext = () => {
    next();
    clearInterval(interval);
  };
  const btnPrev = () => {
    prev();
    clearInterval(interval);
  };

  let isNavHidden = false;
  function handleMouseOver() {
    isNavHidden = !isNavHidden;
  }
</script>

{#each [realisations[index]] as real (index)}
  <div class="container-carousel w-screen lg:w-[55vw] absolute">
    <a href={"/realisations/" + real.attributes.slug} class="link">
      <!-- svelte-ignore a11y-mouse-events-have-key-events -->
      <img
        src={real.attributes.miniature.data.attributes.url}
        transition:fade
        alt=""
        class="img-carousel z-5 max-h-['510px']"
        on:mouseover={handleMouseOver}
      />
    </a>

    <div
      transition:fade
      class="nav-caroussel flex flex-row items-end justify-between {isNavHidden ==
      true
        ? 'opacity-0'
        : 'opacity-100'}"
    >
      <button
        class="arrow-icon left-0 top-0 h-10 w-10 p-[10px] lg:ml-[-1.5em] mt-[-.5em] radius-5"
        on:click={btnPrev}
      >
        <img class=" " src="/arrow_left.svg" alt="précédent" />
      </button>
      <button
        class="arrow-icon right-0 top-0 h-10 w-10 p-[10px] relative lg:mr-[-1.5em] mt-[-.5em] radius-5"
        on:click={btnNext}
      >
        <img class=" scale-x-[-1] " src="/arrow_left.svg" alt="suivant" />
      </button>
    </div>
  </div>
{/each}

<style lang="scss">
  .container-carousel {
    button {
      border-radius: 30px;
      background-color: #E2E9E9;
      transition: transform ease-in 0.1s;
      //background: linear-gradient(51.03deg, rgba(248, 241, 88, 0) -10.35%, rgba(248, 241, 88, 0.2) -5.3%, rgba(178, 236, 194, 0.3722) 23.92%, rgba(153, 243, 255, 0.6459) 60.2%, rgba(130, 247, 255, 0.8643) 72.08%, #79FFFF 85.02%, #79FFFF 85.03%);
    }
    .arrow-icon:active {
      transform: scale(0.8);
    }
    .arrow-icon::before {
      position: absolute;
      content: "";
      height: 1.25rem;
      width: 1.25rem;
      margin-left: -10px;
    }
    .nav-caroussel {
      transition: opacity 0.3s;
      -webkit-transition: opacity 0.3s;
    }
  }
</style>
