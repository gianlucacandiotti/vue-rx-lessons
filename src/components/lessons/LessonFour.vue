<template>
  <section>
    <p>{{people$}}</p>
  </section>
</template>

<script>
import { from } from "rxjs";
import { pluck } from "rxjs/operators";

export default {
  subscriptions() {
    const people$ = from(
      this.$http.get("https://starwars.egghead.training/people/1"),
    ).pipe(pluck("data", "name"));

    return {
      people$,
    };
  },
};
</script>

<style>
</style>
