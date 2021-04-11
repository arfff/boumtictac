<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <!-- <v-card flat> -->
        <v-img contain
               class="mb-5"
               style="max-height:70vh"
               alt="Vue logo"
               src="../assets/bomb_PNG26.png" />
        <!-- <v-card-actions>
            <v-spacer /> -->
        <v-btn text
               depressed
               x-large
               @click="playAllSounds"
               class="mt-5"
               :disabled="startdisabled">
          <span class="display-3">Go !</span>
        </v-btn>
        <!-- </v-card-actions>
        </v-card> -->
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'Bomb',
  data: () => ({
    startdisabled: false,
  }),
  methods: {
    playAllSounds() {
      const that = this;
      // const ticAudio = new Audio('http://www.x-3-x.net/vrml/archive/cache/jeffreykbedrick.com/3d/office/ticktock.wav');
      /* eslint-disable global-require */
      // eslint-disable-next-line import/no-unresolved
      const ticAudio = new Audio(require('../assets/ticktock.wav'));
      const explosionAudio = new Audio(require('../assets/explosion.wav'));
      // const ticAudio = new Audio('@/assets/tictock.wav');
      // const explosionAudio = new Audio('@/assets/explosion.wav');

      const maxticCount = Math.floor(Math.random() * Math.floor(20)) + 10;
      let ticCount = 0;
      ticAudio.addEventListener('ended', () => {
        this.currentTime = 0;
        ticCount += 1;
        if (ticCount < maxticCount) {
          ticAudio.play();
        } else {
          that.startdisabled = false;
          explosionAudio.play();
        }
      }, false);
      ticAudio.addEventListener('canplaythrough', () => {
        /* the audio is now playable; play it if permissions allow */
        that.startdisabled = true;
        ticAudio.play();
      });
      // ticAudio.play();
    },
    playSound(sound) {
      if (sound) {
        const myAudioElement = new Audio(sound);
        myAudioElement.addEventListener('canplaythrough', () => {
          /* the audio is now playable; play it if permissions allow */
          myAudioElement.play();
        });
        // audio.play();
      }
    },
    playTic() {
      this.playSound('@/assets/tictock.wav');
    },
    playBoum() {
      this.playSound('@/assets/explosion.wav');
    },
    countDownTimer() {
      const that = this;
      if (this.countDown === -10) {
        this.setNewTimer();
        setTimeout(() => {
          this.countDownTimer();
        }, 750);
      } else if (this.countDown > 0) {
        setTimeout(() => {
          this.playTic();
          this.countDown -= 1;
          this.countDownTimer();
        }, 650);
      } else {
        setTimeout(() => {
          this.playBoum();
          that.startdisabled = false;
        }, 650);
      }
    },
    start() {
      this.startdisabled = true;
      this.countDown = -10;
      // this.setNewTimer();
      this.countDownTimer();
    },
    setNewTimer() {
      this.countDown = Math.floor(Math.random() * Math.floor(20)) + 10;
    },
  },
};
</script>

<style scoped>
</style>
