<template>
    <div id="my-drum-machine">
      <h1 class="neon-text">My Drum Machine</h1>
      <div class="neon-display" id="display">{{ displayText }}</div>
      <div class="buttons">
        <button
          v-for="button in buttons"
          :key="button.key"
          :class="['neon-button']"
          @click="play(button.key)"
        >
          {{ button.key }}
          <audio :id="button.key" :src="button.audio"></audio>
        </button>
      </div>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, reactive } from "vue";
  
  export default defineComponent({
    name: "DrumMachine",
    setup() {
      const state = reactive({
        displayText: "Click a button to play!",
        buttons: [
          { key: "Q", audio: "/assets/Q.mp3" },
          { key: "W", audio: "/assets/W.mp3" },
          { key: "E", audio: "/assets/E.mp3" },
          { key: "A", audio: "/assets/A.mp3" },
          { key: "S", audio: "/assets/S.mp3" },
          { key: "D", audio: "/assets/D.mp3" },
          { key: "Z", audio: "/assets/Z.mp3" },
          { key: "X", audio: "/assets/X.mp3" },
          { key: "C", audio: "/assets/C.mp3" },
        ],
      });
  
      const play = (key: string) => {
        state.displayText = getDisplayMessage(key);
        const audioElement = document.getElementById(key) as HTMLAudioElement;
        if (audioElement) {
          audioElement.play();
        }
      };
  
      const getDisplayMessage = (key: string) => {
        const messages: Record<string, string> = {
          Q: "Rock on!",
          W: "Drum Roll!",
          E: "Music Time!",
          A: "Big Hit!",
          S: "Party On!",
          D: "Jamming on!",
          Z: "Popstarts!",
          X: "On the mood!",
          C: "On the rythm!",
        };
        return messages[key.toUpperCase()] || "Click a button to play!";
      };
  
      window.addEventListener("keyup", (event) => {
        play(event.key.toUpperCase());
      });
  
      return {
        ...state,
        play,
      };
    },
  });
  </script>
  
  <style scoped>
  .buttons {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
  }
  </style>
  