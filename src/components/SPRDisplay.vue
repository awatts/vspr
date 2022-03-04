<template>
  <div>
    <svg version="1.1"
         baseProfile="full"
         width="900" height="500"
         xlmns="http://www.w3.org/2000/svg">
      <rect width="100%" height="100%" fill="gray"/>
      <text x="425" y="250"
            textlength="800" text-anchor="middle" lengthAdjust="spacingAndGlyphs"
            fill="white">
        {{dashedWords}}
      </text>
    </svg>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Provide, Vue, Watch } from 'vue-property-decorator';
import zip from 'lodash/zip';
import { fromEvent } from 'rxjs';
import { filter, take } from 'rxjs/operators';


@Component
export default class SPRDisplay extends Vue {
  @Prop() private words!: string[];
  private index = -1;

  private timeStamps: number[] = [];
  private responseTimes: number[] = [];

  // In the real finished product, this would be a global and
  // each component would subscribe as needed
  private source = fromEvent<KeyboardEvent>(document, 'keypress');

  private eventSubscription = this.source.pipe(
    filter( (event) => event.key === ' '),
    take(this.words.length + 1),
  ).subscribe({
    next: (v) => this.nextWord(v),
    error: (e) => console.log(e),
    complete: () => this.logTimeStamps(),
  });

  // @Watch('index')
  // private onChildChanged(val: number, oldVal: number) {
  //   console.log(val);
  //  }

  get dashedWords(): string {
    return this.words.map((e, i) => {
      if (i !== this.index) {
        return '–'.repeat(e.length);
      } else {
        return e;
      }
    }).join(' ');
  }

  private nextWord(event: KeyboardEvent) {
    event.preventDefault();
    event.stopPropagation();
    this.timeStamps.push(event.timeStamp);
    this.index++;
  }

  private logTimeStamps() {
    console.log(this.timeStamps);
    this.calculateResponseTimes();
    console.log(this.responseTimes);
  }

  private calculateResponseTimes() {
    this.timeStamps.forEach((x: number, i: number, a: number[]) => {
      if (i > 0) {
        this.responseTimes.push(x - a[i - 1]);
      }
    });
  }

  private resetTrial() {
    this.index = -1;
  }

}
</script>

<style scoped lang="scss">

  svg {
     background-color: #cccccc;
  }

  text {
    font-family: 'Droid Sans Mono', monospace;
    font-size: 24px;
  }
</style>
