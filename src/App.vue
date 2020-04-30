<template>
  <div id="app">
    <Header />
    <section class="cnt-dz">
      <div class="cnt-dz__block">
        <h1 class="cnt-dz__title">Leezy Boost 103</h1>
        <CountDownTimer date="04/30/2020" :schema="schema" />
        <p class="cnt-dz__text">Until Drop</p>
      </div>
    </section>
  </div>
</template>

<script>
import Header from '@/components/Header'
import CountDownTimer from '@/components/CountDownTimer'

export default {
  data() {
    return {
      schema: {
        days: 'Days',
        hours: 'Hours',
        minutes: 'Mins',
        seconds: 'Secs',
      },
    }
  },
  components: {
    Header,
    CountDownTimer,
  },
}
</script>

<style lang="scss">
@import '@/scss/_variables.scss';

* {
  box-sizing: border-box;
}

body {
  background-image: url('./assets/landing.jpg');
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
  font-family: $roboto;
  font-size: 1.4rem;
  line-height: 1.6;
  margin: 0;
  padding: 0;
}

#app {
  height: 100vh;
}

.cnt-dz {
  text-align: right;

  @media #{$mobile} {
    padding-top: 8rem;
    text-align: center;
  }

  &__block {
    display: inline-block;
    margin-right: 10%;

    @media #{$mobile} {
      margin-right: 0;
    }
  }

  &__title {
    font-size: 3rem;
    font-weight: 900;
    margin: 6rem 0 1rem 0;
    text-transform: uppercase;
    letter-spacing: 0.4rem;
    text-align: center;

    @media #{$mobile} {
      font-size: 1.25rem;
    }
  }

  &__text {
    font-size: 1.2rem;
    letter-spacing: 0.25rem;
    text-transform: uppercase;
    text-align: center;

    @media #{$mobile} {
      font-size: 1.1rem;
      margin-top: 0.5rem;
    }
  }
}
</style>
