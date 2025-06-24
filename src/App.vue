<template>
  <div id="app">
    <h1>国男大冒险</h1><div id="waline"></div>
    <event
      v-if="!gameover && currentEvent"
      :event-data="currentEvent"
      @player-choice="handlePlayerChoice"
    ></event>
    <result
      v-if="gameover && currentResultData"
      :result-data="currentResultData"
      @restart-game="afresh"
    ></result>
    <el-dialog title="关于" :visible.sync="dialogVisible2" >
      <div>本项目来源于<a href="https://github.com/Fengzi2333">fengzi2333</a>的<a href="https://github.com/Fengzi2333/GuoNanSimulator">GuoNanSimulator</a>项目。<br><br>经<a href="https://github.com/lylelove">lylelove</a>使用Vue重构。</div>
    </el-dialog>
    <el-button class="bottomright" icon="el-icon-info" @click="dialogVisible2 = true"  circle></el-button>
  </div>
</template>

<script>
import Event from './components/event.vue'
import Result from './components/result.vue';
import eventData from './game-data/events.json';
import resultData from './game-data/results.json';

export default {
  name: 'App',
  components: {
    Event,
    Result
  },
  data() {
    return {
      gameover:false,
      gameon:true, // This might be redundant now
      gamesence:0,
      dialogVisible2: false,
      event_list: eventData,
      result_list: resultData,
      finalResultId: null, // To store the ID of the result when game over
    }
  },
  computed: {
    currentEvent() {
      if (this.event_list && this.event_list.length > 0 && this.gamesence >= 0 && this.gamesence < this.event_list.length) {
        return this.event_list[this.gamesence];
      }
      return null;
    },
    currentResultData() {
      if (!this.gameover || !this.currentEvent) return null;

      // Determine which choice led to the game over to find the correct result ID
      // This assumes that if it's gameover, currentEvent still holds the event that *led* to the gameover.
      // We need to know which button was "conceptually" pressed.
      // This part is tricky because handlePlayerChoice doesn't explicitly store which choice (btn1res/btn2res) led to gameover.
      // For now, let's assume the result ID is stored in a temporary variable or can be inferred.
      // A cleaner way would be to store the resulting ID in a data property when gameover is set.
      // Let's simplify for now and assume the last event's btn1res or btn2res IS the result id.
      // This might need refinement based on how `handlePlayerChoice` sets `gameover`.

      // Attempt to find the result based on the currentEvent's btn1res or btn2res.
      // This is a placeholder logic and might be incorrect.
      // The actual result ID should be determined more robustly in handlePlayerChoice.
      // For now, we'll try to find a result that matches either of the current event's outcome IDs.
      // This is not ideal, as we don't know *which* choice led to the gameover state just by looking at currentEvent.

      // Let's add a temporary data property to store the actual result ID when gameover happens.
      // This will be set in handlePlayerChoice.
      if (this.finalResultId) {
        return this.result_list.find(r => r.id === this.finalResultId);
      }
      return null;
    }
  },
  methods:{
    afresh(){
      this.gameover=false;
      this.gameon=true;
      this.gamesence=0;
      // Data for event component is now passed via props based on currentEvent.
      // The direct modification of this.$refs.event is no longer needed here for afresh.
    },
    handlePlayerChoice(choiceKey) {
      if (!this.currentEvent) {
        console.warn("handlePlayerChoice called with no currentEvent.");
        return;
      }

      const nextId = this.currentEvent[choiceKey];
      if (!nextId) {
        console.warn(`No nextId found for choiceKey: ${choiceKey} in event:`, this.currentEvent);
        // Optionally, set a default error state or message for the user
        this.gameover = true;
        this.finalResultId = "_ERROR_NO_NEXT_ID_"; // Special ID for a generic error result
        return;
      }

      let foundNextEvent = false;

      // Try to find the next event
      const nextEvent = this.event_list.find(event => event.id === nextId);
      if (nextEvent) {
        this.gamesence = this.event_list.indexOf(nextEvent);
        foundNextEvent = true;
      }

      // If no next event, it must be a result
      if (!foundNextEvent) {
        const result = this.result_list.find(r => r.id === nextId);
        if (result) {
          this.gameover = true;
          this.finalResultId = nextId;
        } else {
          console.warn(`Result not found for ID: ${nextId}. Current event:`, this.currentEvent);
          // Set a generic error result if the specific result ID is not found
          this.gameover = true;
          this.finalResultId = "_ERROR_RESULT_NOT_FOUND_";
        }
      }
    },
    // btnfun1 and btnfun2 are no longer needed as event.vue emits 'player-choice'
    // which is directly handled by handlePlayerChoice in the template.
    // We can remove them if they are not used elsewhere (e.g. legacy calls).
    // For now, let's assume they are effectively replaced.
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.none{
  display: none;
}
.bottomleft{
  position: fixed;
  bottom: 0;
  left: 0;
}
.bottomright{
  position: fixed;
  bottom: 0;
  right: 0;
}
</style>
