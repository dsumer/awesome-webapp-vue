<template>
  <div class="wrapper">
    ahoi!
    <br/>
    Stars Count (Server Side): {{ serverSideStars }}
    <br/>
    Stars Count (Client Side): {{ clientSideStars }}
  </div>
</template>

<script>
import fetch from 'isomorphic-unfetch';

const fetchStars = async () => {
  const res = await fetch('https://api.github.com/repos/zeit/next.js')
  const json = await res.json()
  return json.stargazers_count
}

export default {
  data() {
    return {
      clientSideStars: 0
    }
  },
  async asyncData() {
    const serverSideStars = await fetchStars();
    return {
      serverSideStars
    }
  },
  async mounted() {
    const clientSideStars = await fetchStars();
    this.clientSideStars = clientSideStars;
  }
}
</script>

<style>
  .wrapper {
    text-align: center;
  }
</style>
