<template>
  <div @click="nextWord" id=sprwords>
    <svg version="1.1"
         baseProfile="full"
         width="900" height="500"
         xlmns="http://www.w3.org/2000/svg">
      <rect width="100%" height="100%" fill="gray"/>
      <text x="425" y="250" font-size="32" 
            textlength="800" text-anchor="middle" lengthAdjust="spacingAndGlyphs"
            fill="white">
        {{dashedWords}}
      </text>
    </svg>
    <button type="button" name="reset" @click.stop="resetTrial">Reset</button>
  </div>
</template>

<script lang="ts">
import { Component, Provide, Vue, Watch } from 'vue-property-decorator';
import zip from 'lodash/zip';

@Component
export default class SPRDisplay extends Vue {
  @Provide() private words: string[] = ['the', 'quick', 'brown', 'fox', 'jumps',
                                        'over', 'the', 'lazy', 'dog'];
  @Provide() private index: number = -1;

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

  private nextWord() {
    this.index++;
  }

  private resetTrial() {
    this.index = -1;
  }

}
</script>

<style scoped lang="scss">

  #sprwords {
    background-color: #cccccc;
    font: monospace;
  }
</style>
