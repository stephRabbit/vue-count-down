<template>
  <div class="cdt-dz-item">
    <p v-for="(item, index) in data" :key="index" class="cdt-dz-item__number">
      {{ item }}
    </p>
    <p class="cdt-dz-item__label">{{ label }}</p>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
    },
    data: {
      type: Array,
      required: true,
    },
  },
}
</script>

<style lang="scss" scoped>
@import '@/scss/_variables.scss';

.cdt-dz-item {
  display: inline-block;
  margin: 0 0.5rem;
  text-align: center;

  @media #{$mobile} {
    margin: 0 0.25rem;
  }

  &__number {
    background-color: $black;
    color: $white;
    display: inline-block;
    font-family: $rozhaOne;
    font-size: 3rem;
    font-weight: normal;
    letter-spacing: 0.5rem;
    line-height: 4.5rem;
    margin: 0 0.35rem;
    padding: 0 0.25rem 0 0.75rem;
    width: 55px;

    @media #{$mobile} {
      font-size: 1.25rem;
      line-height: 3rem;
      margin: 0 0.1rem;
      padding: 0 0.25rem 0 0.75rem;
      width: 35px;
    }
  }

  &__label {
    font-weight: bold;
    letter-spacing: 0.25rem;
    text-transform: uppercase;

    @media #{$mobile} {
      font-size: 0.9rem;
      margin-top: 0.25rem;
    }
  }
}
</style>
