<template>
  <section>
    <button v-stream:click="click$">Click</button>
    <p>{{random$}}</p>
  </section>
</template>

<script>
import { map } from "rxjs/operators";

export default {
  domStreams: ["click$"],
  subscriptions() {
    const random$ = this.click$.pipe(map(() => Math.random()));

    return {
      random$,
    };
  },
};
</script>

<style>
</style>
