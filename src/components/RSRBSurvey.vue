<template>
    <div id="rsrb">
        <h3>{{lab}} Laboratory Participant Questionnaire</h3>
        <p>This is an optional questionnaire. Answering this questionnaire will not affect your participation in this study, nor will it affect your payment for participation in this study. You may answer some of these questions, all of these questions, or none of these questions. The questions are designed for one of two things:</p>
        <ol>
            <li>Provide us with information that will better help us conduct the experiment and analyze the data from the experiment.</li>
            <li>Provide us with information regarding participant demographics (age, race, sex, etc.) that is often requested by groups monitoring and/or funding our research. This information is requested by groups such as the National Science Foundation (NSF), the National Institute of Health (NIH), and the university's Research Review Board (RSRB) to ensure that human research studies accurately sample the population base of the region. This also helps to make sure that certain population subsets (minorities, females, etc.) are no longer wittingly or unwittingly underrepresented in scientific research data.</li>
        </ol>
        <p>If after you complete and submit this questionnaire you later decide that you wish to amend or erase any information you supplied us, please let us know, as you are always free to make changes to this info.</p>
        <ol>
            <li>Age
                <input type="number" min="0" max="100" step="1" name="rsrb.age"/>
            </li>
            <li>Sex
                <select name="rsrb.sex">
                    <option value="NA" selected>N/A</option>
                    <option value="Male">Male</option>
                    <option value="Female">Female</option>
                </select>
            </li>
            <li>Ethnicity
                <select name="rsrb.ethnicity">
                    <option value="NA" selected>N/A</option>
                    <option value="Hisp">Hispanic or Latino</option>
                    <option value="NonHisp">Not Hispanic or Latino</option>
                </select>
            </li>
            <li>Race (you may check more than one)
                <ul>
                    <li><input type="checkbox" name="rsrb.race" id="race_amerind" value="amerind;"/><label for="race_amerind">American Indian / Alaska Native</label></li>
                    <li><input type="checkbox" name="rsrb.race" id="race_black" value="black;"/><label for="race_black">Black or African-American</label></li>
                    <li><input type="checkbox" name="rsrb.race" id="race_pacif" value="pacif;"/><label for="race_pacif">Native Hawaiian or Other Pacific Islander</label></li>
                    <li><input type="checkbox" name="rsrb.race" id="race_asian" value="asian;"/><label for="race_asian">Asian</label></li>
                    <li><input type="checkbox" name="rsrb.race" id="race_white" value="white;"/><label for="race_white">White</label></li>
                    <li><input type="checkbox" name="rsrb.race" id="race_unknown" value="unknown;"/><label for="race_unknown">Unknown</label></li>
                    <li><input type="checkbox" name="rsrb.race" id="race_other" value="other;"/><label for="race_other">Other</label></li>
                If Other:
                <input type="text" name="rsrb.raceother"/>
                </ul>
            </li>
        </ol>
        <input type="hidden" name="rsrb.protocol" :value="protocol" />
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class RSRBSurvey extends Vue {
    @Prop() private protocol!: string;
    @Prop() private lab!: string;
}
</script>

<style scoped lang="scss">
</style>
