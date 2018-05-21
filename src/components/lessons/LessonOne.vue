<template>
  <section>
    <p>{{interval$}}</p>
  </section>
</template>

<script>
import { interval } from "rxjs";

export default {
  subscriptions: {
    interval$: interval(1000),
  },
};
</script>
