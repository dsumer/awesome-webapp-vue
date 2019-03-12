<template>
  <div class="wrapper">
    <p>
      ahoi!
    </p>
    <p>
      Greeting (Server Side): {{ serverSideGreeting }}
    </p>
    <p>
      Greeting (Client Side): {{ clientSideGreeting }}
    </p>
    <p>
      <input type="text" v-model="localName" /> <button @click="changeName()">Change Name</button>
    </p>
    <p>
      <nuxt-link to="/second" no-prefetch>Go to the second page</nuxt-link>
    </p>
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
  p {
    margin-top: 0;
  }
</style>
