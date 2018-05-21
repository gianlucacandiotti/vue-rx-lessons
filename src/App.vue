<template>
  <div class="app">
    <h1 class="title">Vue.js with RxJS showcase</h1>

    <div class="lessons">
      <Lesson title="Lesson 1: Single Interval">
        <lesson-one />
      </Lesson>
      <Lesson title="Lesson 2: Multiple intervals">
        <lesson-two />
      </Lesson>
      <Lesson title="Lesson 3: Access Events as RxJS Streams">
        <lesson-three />
      </Lesson>
      <Lesson title="Lesson 4: Stream an API using RxJS">
        <lesson-four />
      </Lesson>
      <Lesson title="Lesson 5: Map Click Event Streams to load data">
        <lesson-five />
      </Lesson>
      <Lesson title="Lesson 6: Split Request into Data Stream and Image Stream">
        <lesson-six />
      </Lesson>
      <Lesson title="Lesson 7: : Handle Image Loading Errors">
        <lesson-seven />
      </Lesson>
      <Lesson title="Lesson 8: Switch to function which creates Observables">
        <lesson-eight />
      </Lesson>
      <Lesson title="Lesson 9: Catch errors when data fails to load">
        <lesson-nine />
      </Lesson>
      <Lesson title="Lesson 10: Share RxJS Streams to avoid multiple requests">
        <lesson-ten />
      </Lesson>
      <Lesson title="Lesson 11: Disable buttons while data is loading">
        <lesson-eleven />
      </Lesson>
      <Lesson title="Lesson 12: Pause until another Stream completes with exhaustMap">
        <lesson-twelve />
      </Lesson>
      <Lesson title="Lesson 13: Pass template data through domStreams">
        <lesson-thirteen />
      </Lesson>
      <Lesson title="Lesson 14: Watch v-models as Observable">
        <lesson-fourteen />
      </Lesson>
      <Lesson title="Lesson 15: Sync Vue Components with Streaming Content">
        <lesson-fifteen />
      </Lesson>
      <Lesson title="Lesson 16: Map Vue Components to Remote Data Streams">
        <lesson-sixteen />
      </Lesson>
      <Lesson title="Lesson 17: Use Promises">
        <lesson-seventeen />
      </Lesson>
      <Lesson title="Lesson 18: Cache Remove Data Requests">
        <lesson-eighteen />
      </Lesson>
      <Lesson title="Lesson 19: Optimize bundle size by piping operators (All lessons already done using piping because of RxJS 6 so this lesson has no significant changes except for the usage of combineLatest)">
        <lesson-nineteen />
      </Lesson>
    </div>
  </div>
</template>

<script>
import Lesson from "./components/Lesson";
import LessonOne from "./components/lessons/LessonOne";
import LessonTwo from "./components/lessons/LessonTwo";
import LessonThree from "./components/lessons/LessonThree";
import LessonFour from "./components/lessons/LessonFour";
import LessonFive from "./components/lessons/LessonFive";
import LessonSix from "./components/lessons/LessonSix";
import LessonSeven from "./components/lessons/LessonSeven";
import LessonEight from "./components/lessons/LessonEight";
import LessonNine from "./components/lessons/LessonNine";
import LessonTen from "./components/lessons/LessonTen";
import LessonEleven from "./components/lessons/LessonEleven";
import LessonTwelve from "./components/lessons/LessonTwelve";
import LessonThirteen from "./components/lessons/LessonThirteen";
import LessonFourteen from "./components/lessons/LessonFourteen";
import LessonFifteen from "./components/lessons/LessonFifteen";
import LessonSixteen from "./components/lessons/LessonSixteen";
import LessonSeventeen from "./components/lessons/LessonSeventeen";
import LessonEighteen from "./components/lessons/LessonEighteen";
import LessonNineteen from "./components/lessons/LessonNineteen";

export default {
  components: {
    Lesson,
    LessonOne,
    LessonTwo,
    LessonThree,
    LessonFour,
    LessonFive,
    LessonSix,
    LessonSeven,
    LessonEight,
    LessonNine,
    LessonTen,
    LessonEleven,
    LessonTwelve,
    LessonThirteen,
    LessonFourteen,
    LessonFifteen,
    LessonSixteen,
    LessonSeventeen,
    LessonEighteen,
    LessonNineteen,
  },
};
</script>

<style lang="scss" scoped>
.app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.title {
  font-size: 24px;
  text-align: center;
}

.lessons {
  align-items: flex-start;
  border-bottom: 1px solid;
  border-top: 1px solid;
  display: flex;
  flex-direction: column;
}
</style>
