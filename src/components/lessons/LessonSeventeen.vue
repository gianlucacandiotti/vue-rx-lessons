<template>
  <section>
    <div class="tab-container">
      <b-tabs v-model="activeTab">
        <b-tab-item v-for="person of people$" :key="person.id" :label="person.name" />
      </b-tabs>
    </div>

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
  combineLatest,
} from "rxjs/operators";

export default {
  data() {
    return {
      activeTab: 0,
    };
  },
  domStreams: ["click$", "imageError$"],
  subscriptions() {
    const myPromise = new Promise(resolve => {
      console.log("INVOKED");

      resolve(new Date());
    });

    from(myPromise).subscribe(value => console.log(value));
    from(myPromise).subscribe(value => console.log(value));
    from(myPromise).subscribe(value => console.log(value));
    from(myPromise).subscribe(value => console.log(value));

    const createLoader = url => from(this.$http.get(url)).pipe(pluck("data"));

    const people$ = createLoader(
      "https://starwars.egghead.training/people",
    ).pipe(map(people => people.slice(0, 7)));

    const activeTab$ = this.$watchAsObservable("activeTab", {
      immediate: true,
    }).pipe(pluck("newValue"));

    const luke$ = activeTab$.pipe(
      combineLatest(people$, (tabId, people) => people[tabId].id),
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
      people$,
    };
  },
};
</script>

<style lang="scss" scoped>
.tab-container {
  width: 300px;
  max-width: 100%;
}
</style>
