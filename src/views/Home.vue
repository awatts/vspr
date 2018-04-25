<template>
  <div class="home">
    <SPRDisplay />
    <RSRBSurvey lab="Jaeger" protocol="FILL_ME_IN"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import RSRBSurvey from '@/components/RSRBSurvey.vue';
import SPRDisplay from '@/components/SPRDisplay.vue';

@Component({
  components: {
    RSRBSurvey,
    SPRDisplay,
  },
})
export default class Home extends Vue {}
</script>
