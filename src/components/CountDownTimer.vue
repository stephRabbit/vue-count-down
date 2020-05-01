<template>
  <div class="cdt-dz">
    <CountDownItem
      v-for="(item, k, i) in schema"
      :key="i"
      :data="getComputedByName(k)"
      :label="item"
    />
  </div>
</template>

<script>
import CountDownItem from '@/components/CountDownItem'

export default {
  created() {
    this.startCounter()
  },
  data() {
    return {
      now: Math.floor(+new Date() / 1000),
      timer: null,
      defaultTime: '23:59:59',
    }
  },
  props: {
    date: {
      type: String,
      required: true,
    },
    range: {
      type: String,
    },
    schema: {
      type: Object,
      required: true,
    },
  },
  components: {
    CountDownItem,
  },
  methods: {
    startCounter() {
      // Start timer based on distance
      if (this.isDistance) {
        this.timer = setInterval(() => {
          this.now = Math.floor(+new Date() / 1000)
        }, 1000)
      }
    },
    getComputedByName(name) {
      // Get property name by string
      return this[name]
    },
    splitToDigit(n) {
      // Fail gracefully when number is not valid
      if (n < 0 || isNaN(n)) return [0, 0]

      // Add zero for single digits
      if (n.toString().length <= 1) n = `0${n}`

      // Convert to string and spread it into array
      // flip in back to a number - Number callback
      return [...(n + '')].map(Number)
    },
  },
  watch: {
    now(currentVal) {
      // Clear timer once countdown ends
      if (currentVal > this.then) {
        clearInterval(this.timer)
      }
    },
  },
  computed: {
    dateString() {
      // Date string
      return `${this.date} ${this.range || this.defaultTime}`
    },
    then() {
      // Timestamp past in seconds
      return Math.floor(new Date(this.dateString).getTime() / 1000)
    },
    isDistance() {
      // Check if time it time has expired (then > now)
      return this.then > this.now
    },
    distance() {
      // Check length of time (then - now) in seconds
      return this.then - this.now
    },
    seconds() {
      // Distance in seconds divide 60 and get the remainder
      return this.splitToDigit(this.distance % 60)
    },
    minutes() {
      // Distance in seconds divide 60 * 2 and get the remainder
      return this.splitToDigit(Math.floor(this.distance / 60) % 60)
    },
    hours() {
      // Distance in seconds divide 60 * 2 / 24 and get the remainder
      return this.splitToDigit(Math.floor(this.distance / 60 / 60) % 24)
    },
    days() {
      // Distance in seconds divide 60 * 2 / 24
      return this.splitToDigit(Math.floor(this.distance / 60 / 60 / 24))
    },
  },
}
</script>

<style lang="scss" scoped>
.cdt-dz {
  text-align: center;
}
</style>
