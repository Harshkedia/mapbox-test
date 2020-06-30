<template>
  <div>
    Record something here <br />
    <button ref="record" @click="record">Record</button> <br />
    <button ref="stop" @click="stop">Stop</button> <br >
    <audio ref="player" controls :src="audioURL" />
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Record",
  components: {},
  data() {
    return {
      mediaRecorder: null,
      chunks: [],
      audioURL: ""
    };
  },
  computed: {
    recordButton() {
      return this.$refs.record;
    },
    stopButton() {
      return this.$refs.stop;
    },
    player() {
      return this.$refs.player;
    }
  },
  mounted() {
    navigator.mediaDevices.getUserMedia({ audio: true }).then(stream => {
      this.mediaRecorder = new MediaRecorder(stream);
      this.mediaRecorder.ondataavailable = e => {
        this.chunks.push(e.data);
      };

      this.mediaRecorder.onstop = () => {
        console.log("recorder stopped");

        const blob = new Blob(this.chunks, { type: "audio/ogg; codecs=opus" });
        this.chunks = [];

        this.audioURL = window.URL.createObjectURL(blob);
      };
    });
  },
  methods: {
    record() {
      this.mediaRecorder.start();
      console.log(this.mediaRecorder.state);
      console.log("recorder started");
    },
    stop() {
      this.mediaRecorder.stop();
      console.log(this.mediaRecorder.state);
      console.log("recorder stopped");
    }
  }
};
</script>
