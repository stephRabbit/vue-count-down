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
      now: Math.floor(new Date().getTime() / 1000),
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
    splitToDigit(n) {
      // Return [0, 0] for display when number is below 0
      if (n < 0) return [0, 0]

      // Add zero for single digits
      if (n.toString().length <= 1) n = `0${n}`

      // Convert to string and spread it into array
      // flip in back to a number - Number callback
      return [...(n + '')].map(Number)
    },
    startCounter() {
      // Start timer based on distance
      if (this.isDistance) {
        this.timer = setInterval(() => {
          this.now = Math.floor(new Date().getTime() / 1000)
        }, 1000)
      }
    },
    getComputedByName(name) {
      return this[name]
    },
  },
  watch: {
    now(currentVal) {
      if (currentVal > this.ms) {
        clearInterval(this.timer)
      }
    },
  },
  computed: {
    dateTime() {
      return `${this.date} ${this.range || this.defaultTime}`
    },
    ms() {
      return Math.floor(new Date(this.dateTime).getTime() / 1000)
    },
    isDistance() {
      return this.ms > this.now
    },
    distance() {
      return this.ms - this.now
    },
    seconds() {
      return this.splitToDigit(this.distance % 60)
    },
    minutes() {
      return this.splitToDigit(Math.floor(this.distance / 60) % 60)
    },
    hours() {
      return this.splitToDigit(Math.floor(this.distance / 60 / 60) % 24)
    },
    days() {
      return this.splitToDigit(Math.floor((this.ms - this.now) / 60 / 60 / 24))
    },
  },
}
</script>

<style lang="scss" scoped>
.cdt-dz {
  text-align: center;
}
</style>
