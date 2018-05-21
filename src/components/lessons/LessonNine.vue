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
import { from, merge, of } from "rxjs";
import { switchMap, pluck, map, mapTo, catchError } from "rxjs/operators";

export default {
  domStreams: ["click$", "imageError$"],
  subscriptions() {
    const createLoader = url => from(this.$http.get(url)).pipe(pluck("data"));

    const luke$ = this.click$.pipe(
      mapTo("https://starwars.egghead.trainin/people/1"),
      switchMap(createLoader),
      catchError(() => of({ name: "This is an error :(" })),
    );

    const name$ = luke$.pipe(pluck("name"));
    const imageLoad$ = luke$.pipe(
      pluck("image"),
      map(image => `https://starwars.egghead.training/${image}`),
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
