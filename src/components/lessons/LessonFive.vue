<template>
  <section>
    <button v-stream:click="click$">Click</button>
    <p>{{luke$}}</p>
  </section>
</template>

<script>
import { from } from "rxjs";
import { switchMap, pluck } from "rxjs/operators";

export default {
  domStreams: ["click$"],
  subscriptions() {
    const people$ = from(
      this.$http.get("https://starwars.egghead.training/people/1"),
    ).pipe(pluck("data", "name"));
    const luke$ = this.click$.pipe(switchMap(() => people$));

    return {
      luke$,
    };
  },
};
</script>

<style>
</style>
