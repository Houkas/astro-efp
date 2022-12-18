<footer
  class=" sm:pl-0 sm:pr-0 bg-white dashed-footer dashed-footer-top md:flex md:items-center md:justify-between md:pl-20 md:pr-20 "
>
  <div class="container-footer md:flex md:items-center md:justify-between ">
    <span class="text-sm">
      <b>EFP - Entreprise familliale de peinture</b><br />
      <!--EFP4@wanadoo.fr<br />-->
      Sauveterre de Guyenne - 33540 France
    </span>
    <img src="/logo-efp-without-txt.png" class="logo-efp" alt="" />
    <span class="text-sm text-right">
      Peinture intérieur - exterieur - vitrage - sol
    </span>
  </div>
</footer>

<style lang="scss">
  .dashed-footer-top {
    background-image: linear-gradient(
      to right,
      #F8FBFB 66%,
      rgba(255, 255, 255, 0) 0%
    );
    background-position: top;
    background-size: 25px 2px;
    background-repeat: repeat-x;
  }
  .dashed-footer::before {
    content: "";
    position: absolute;
    min-height: 162px;
    width: 2px;
    z-index: 10;
    background-image: linear-gradient(#F8FBFB 66%, rgba(255, 255, 255, 0) 0%);
    background-position: left;
    background-size: 2px 25px;
    background-repeat: repeat-y;
  }
  .dashed-footer::after {
    content: "";
    position: absolute;
    min-height: 162px;
    width: 5px;
    z-index: 10;
    background-image: linear-gradient(#F8FBFB 66%, rgba(255, 255, 255, 0) 0%);
    background-position: right;
    background-size: 2px 25px;
    background-repeat: repeat-y;
    right: 80px;
  }
  footer {
    position: relative;
    z-index: 999;
    min-height: 162px;
    background-color: #E2E9E9;
    font-family: "Zen Kaku Gothic New", sans-serif;

    .container-footer {
      width: 100%;
      margin: 0 auto;
      padding: 10px 33px 10px 33px;
    }

    span {
      font-family: "Zen Kaku Gothic New", sans-serif;
      color: #122023;
    }

    .logo-efp {
      width: 65px;
      height: 65px;
    }
  }
  @media (max-width: 640px) {
    .dashed-footer::after,
    .dashed-footer::before {
      display: none !important;
    }
    footer .logo-efp {
      margin: 10px auto 10px auto;
    }
  }
</style>
