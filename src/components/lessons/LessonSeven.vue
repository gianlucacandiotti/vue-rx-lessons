<template>
  <section>
    <button v-stream:click="click$">Click</button>

    <div>
      <p>{{name$}}</p>
      <img v-if="Boolean(image$)" :src="image$" v-stream:error="imageError$" alt="Image">
    </div>
  </section>
</template>

<script>
import { from, merge } from "rxjs";
import { switchMap, pluck, map, mapTo } from "rxjs/operators";

export default {
  domStreams: ["click$", "imageError$"],
  subscriptions() {
    const person$ = from(
      this.$http.get("https://starwars.egghead.training/people/1"),
    ).pipe(pluck("data"));
    const luke$ = this.click$.pipe(switchMap(() => person$));

    const name$ = luke$.pipe(pluck("name"));
    const imageLoad$ = luke$.pipe(
      pluck("image"),
      // Put a bad url on purpose to force the error
      map(image => `https://starwars.egghead.trainin/${image}`),
    );
    const failImage$ = this.imageError$.pipe(
      mapTo("http://via.placeholder.com/200x200"),
    );
    const image$ = merge(imageLoad$, failImage$);

    return {
      name$,
      image$,
    };
  },
};
</script>
