<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>

<script>

export default {
  props: ['id'],
  computed: {
    event () {
      return this.$store.state.event
    }
  },
  created () {
    this.$store.dispatch('fetchEvent', this.id).catch(err => {
      this.$router.push({
        name: 'ErrorDisplay',
        params: {
          error: err.code
        }
      })
    })
  }


}
</script>