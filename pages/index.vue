<template>
  <div class="wrapper">
    ahoi!
    <br/>
    Greeting (Server Side): {{ serverSideGreeting }}
    <br/>
    Greeting (Client Side): {{ clientSideGreeting }}
    <br/>
    <input type="text" v-model="localName" /> <button @click="changeName()">Change Name</button>
  </div>
</template>

<script>
const fetchStars = async ($axios) => {
  const res = await $axios.$get('/api/greeting')
  return res
}

export default {
  data() {
    return {
      clientSideGreeting: 0,
      localName: ''
    }
  },
  async asyncData({$axios}) {
    const serverSideGreeting = await fetchStars($axios);
    return {
      serverSideGreeting
    }
  },
  async mounted() {
    const clientSideGreeting = await fetchStars(this.$axios);
    this.clientSideGreeting = clientSideGreeting;
  },
  methods: {
    async changeName() {
      const res = await this.$axios.$post('/api/greeting', this.localName, {headers: {"Content-Type": "text/plain"}})
      console.log(res)
    }
  }
}
</script>

<style>
  .wrapper {
    text-align: center;
  }
</style>
