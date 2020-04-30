<template>
  <div class="hdr-dz">
    <header class="hdr-dz__wrap">
      <div class="hdr-dz__logo">
        <span class="hdr-dz__text-wrap hdr-dz__text-wrap--pull-left">DROP</span>
        <span class="hdr-dz__text-wrap hdr-dz__text-wrap--left">ZONE</span>
      </div>
    </header>
  </div>
</template>

<style lang="scss" scoped>
@import '@/scss/_variables.scss';

.hdr-dz {
  border-top: 20px solid $black;

  @media #{$mobile} {
    border-top: 0;
  }

  &__wrap {
    display: grid;
    grid-template-columns: 1fr 3fr;
    grid-template-areas: 'gap logo';
    justify-items: end;
  }

  &__logo {
    font-family: $rozhaOne;
    font-size: 2.25rem;
    grid-area: logo;
    margin: 2rem;
    width: 131px;
    line-height: 1.3;
  }

  &__text-wrap {
    background-color: $black;
    color: $white;
    display: inline-block;
    font-weight: normal;
    letter-spacing: 0.5rem;
    margin-bottom: 0.5rem;
    padding: 0 0.25rem 0 0.75rem;
  }

  &__text-wrap--pull-left {
    margin-left: -1.5rem;
  }
}
</style>
