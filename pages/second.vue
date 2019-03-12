<template>
  <div class="wrapper">
    Rolled number: {{ number }} <button @click="rollDice()">Roll the dice</button>
    <br/>
    <nuxt-link to="/" no-prefetch>Go back</nuxt-link>
  </div>
</template>

<script>
  import Roll from 'roll';
  const roll = new Roll();

  export default {
    data() {
      return {
        number: 0
      }
    },
    methods: {
      rollDice() {
        this.number = roll.roll('d6').result;
      }
    }
  }
</script>

<style>
  .wrapper {
    text-align: center;
  }
</style>
