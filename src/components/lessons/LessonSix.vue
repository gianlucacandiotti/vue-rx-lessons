<template>
  <section>
    <button v-stream:click="click$">Click</button>

    <div>
      <p>{{name$}}</p>
      <img v-if="Boolean(image$)" :src="image$" alt="Image">
    </div>
  </section>
</template>

<script>
import { from } from "rxjs";
import { switchMap, pluck, map } from "rxjs/operators";

export default {
  domStreams: ["click$"],
  subscriptions() {
    const person$ = from(
      this.$http.get("https://starwars.egghead.training/people/1"),
    ).pipe(pluck("data"));
    const luke$ = this.click$.pipe(switchMap(() => person$));

    const name$ = luke$.pipe(pluck("name"));
    const image$ = luke$.pipe(
      pluck("image"),
      map(image => `https://starwars.egghead.training/${image}`),
    );

    return {
      name$,
      image$,
    };
  },
};
</script>
