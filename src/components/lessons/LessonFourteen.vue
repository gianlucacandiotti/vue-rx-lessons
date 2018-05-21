<template>
  <section>
    {{activeTab$}}
    <b-tabs v-model="activeTab">
      <b-tab-item label="Luke"></b-tab-item>
      <b-tab-item label="Darth"></b-tab-item>
      <b-tab-item label="Leia"></b-tab-item>
    </b-tabs>

    <button v-stream:click="{ subject: click$, data: 1 }">{{buttonText$}}</button>
    <button v-stream:click="{ subject: click$, data: 4 }">{{buttonText$}}</button>
    <button v-stream:click="{ subject: click$, data: 5 }">{{buttonText$}}</button>

    <div>
      <p>{{name$}}</p>
      <img v-if="Boolean(image$)" :src="image$" v-stream:error="imageError$" alt="Image">
    </div>
  </section>
</template>

<script>
import { from, merge, of } from "rxjs";
import {
  exhaustMap,
  pluck,
  map,
  mapTo,
  catchError,
  share,
  startWith,
} from "rxjs/operators";

export default {
  data() {
    return {
      activeTab: 0,
    };
  },
  domStreams: ["click$", "imageError$"],
  subscriptions() {
    const activeTab$ = this.$watchAsObservable("activeTab", {
      immediate: true,
    }).pipe(pluck("newValue"));

    const createLoader = url => from(this.$http.get(url)).pipe(pluck("data"));

    const luke$ = this.click$.pipe(
      pluck("data"),
      map(id => `https://starwars.egghead.training/people/${id}`),
      // Test this in slowing requests in performance tab and checking requests
      // waterfall in network tab
      exhaustMap(createLoader),
      catchError(() => of({ name: "This is an error :(" })),
      share(),
    );

    const disabled$ = merge(
      this.click$.pipe(mapTo(true)),
      luke$.pipe(mapTo(false)),
    ).pipe(startWith(false));

    const buttonText$ = disabled$.pipe(
      map(bool => (bool ? "Loading..." : "Load")),
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
      disabled$,
      buttonText$,
      activeTab$,
    };
  },
};
</script>
