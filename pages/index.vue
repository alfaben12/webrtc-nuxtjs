<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12 my-3">
        <h2 class="text-blue-500">Room</h2>
        <input v-if="false" v-model="roomId" />
        <input class="form-control" value="thariq-alfa-tes-v2" readonly />
      </div>
    </div>
    <div class="flex flex-col">
      <div class="">
        <div class="flex space-x-3">
          <div>
            <vue-webrtc
              ref="webrtc"
              width="30%"
              :room-id="roomId"
              @joined-room="logEvent"
              @left-room="logEvent"
              @opened-room="logEvent"
              @share-started="logEvent"
              @share-stopped="logEvent"
              @error="onError"
            />
          </div>
          <div v-if="shareScreen !== null">
            <figure class="figure">
              <img :src="shareScreen" class="w-28" />
            </figure>
          </div>
        </div>
        <div class="row">
          <div class="col-md-12 my-3">
            <button
              type="button"
              class="
                bg-blue-500
                hover:bg-blue-700
                text-white
                font-bold
                py-2
                px-4
                rounded
              "
              @click="onJoin"
            >
              Join
            </button>
            <button
              type="button"
              class="
                bg-blue-500
                hover:bg-blue-700
                text-white
                font-bold
                py-2
                px-4
                rounded
              "
              @click="onLeave"
            >
              Leave
            </button>
            <button
              type="button"
              class="
                bg-blue-500
                hover:bg-blue-700
                text-white
                font-bold
                py-2
                px-4
                rounded
              "
              @click="onCapture"
            >
              Capture Photo
            </button>
            <button
              type="button"
              class="
                bg-blue-500
                hover:bg-blue-700
                text-white
                font-bold
                py-2
                px-4
                rounded
              "
              @click="onShareScreen"
            >
              Share Screen
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <h2>Captured Image</h2>
        <figure class="figure">
          <img :src="img" class="img-responsive" />
        </figure>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { WebRTC } from 'vue-webrtc'
Vue.component(WebRTC.name, WebRTC)

export default {
  data() {
    return {
      img: null,
      shareScreen: null,
      roomId: 'public-room-v2',
    }
  },
  computed: {},
  watch: {},
  methods: {
    onCapture() {
      this.img = this.$refs.webrtc.capture()
    },
    onJoin() {
      this.$refs.webrtc.join()
    },
    onLeave() {
      this.$refs.webrtc.leave()
    },
    onShareScreen() {
      this.img = this.$refs.webrtc.shareScreen()
    },
    onError(error, stream) {
      console.log('On Error Event', error, stream)
    },
    logEvent(event) {
      console.log('Event : ', event)
    },
  },
}
</script>
