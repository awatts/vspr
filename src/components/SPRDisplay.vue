<template>
  <div id=sprwords>
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
import { Component, Provide, Vue, Watch } from 'vue-property-decorator';
import zip from 'lodash/zip';
import { Observable } from 'rxjs';
import { filter, take } from 'rxjs/operators';


@Component
export default class SPRDisplay extends Vue {
  private words: string[] = ['the', 'quick', 'brown', 'fox', 'jumps',
                                        'over', 'the', 'lazy', 'dog'];
  private index: number = -1;

  private timeStamps: number[] = [];
  private responseTimes: number[] = [];

  // In the real finished product, this would be a global and
  // each component would subscribe as needed
  private source = Observable.fromEvent<KeyboardEvent>(document, 'keypress');

  private eventSubscription = this.source.pipe(
    filter( (event) => event.charCode === 32),
    take(this.words.length + 1),
  ).subscribe(
    (event) => this.nextWord(event),
    (error) => console.log(error),
    () => this.logTimeStamps(),
    );

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
  }
  private resetTrial() {
    this.index = -1;
  }

}
</script>

<style scoped lang="scss">

  text {
    font-family: 'Droid Sans Mono', monospace;
    font-size: 24px;
  }

  #sprwords {
    background-color: #cccccc;
    font: monospace;
  }
</style>
