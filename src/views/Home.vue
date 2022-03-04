<template>
  <div class="home">
    <SPRDisplay v-bind:words="['the', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import SPRDisplay from '@/components/SPRDisplay.vue';

@Component({
  components: {
    SPRDisplay,
  },
})
export default class Home extends Vue {}
</script>
