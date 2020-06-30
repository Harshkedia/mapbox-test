<template>
  <div>
    Record something here <br />
    <button ref="record" @click="record">Record</button> <br />
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
      audioURL: "",
      position: {}
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
    this.getCurrentPosition();

    navigator.mediaDevices.getUserMedia({ audio: true }).then(stream => {
      this.mediaRecorder = new MediaRecorder(stream);

      // Add chunks whenever data is available
      this.mediaRecorder.ondataavailable = e => {
        this.chunks.push(e.data);
      };

      // Create url when recording stops
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
      setTimeout(this.stop, 4000);
    },
    stop() {
      this.mediaRecorder.stop();
      console.log(this.mediaRecorder.state);
      console.log("recorder stopped");
    },
    getCurrentPosition() {
      navigator.geolocation.getCurrentPosition(position => {
        this.position = { long: position.coords.longitude, lat: position.coords.latitude };
      });
    }
  }
};
</script>
