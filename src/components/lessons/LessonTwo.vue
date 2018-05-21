<template>
  <section>
    <p>{{timesTwo$}}</p>
    <p>{{timesThree$}}</p>
  </section>
</template>

<script>
import { interval } from "rxjs";
import { map } from "rxjs/operators";

export default {
  subscriptions() {
    const interval$ = interval(1000);

    const timesTwo$ = interval$.pipe(map(i => i * 2));
    const timesThree$ = interval$.pipe(map(i => i * 3));

    return {
      timesTwo$,
      timesThree$,
    };
  },
};
</script>
