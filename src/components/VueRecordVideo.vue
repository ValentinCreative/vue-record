<template lang="html">
  <div
    v-if="isSupported"
    class="vue-video-recorder"
    :class="{
      'active': isRecording,
      'paused': isPaused
    }"
    @mousedown="startRecording"
    @mouseleave="stopRecording"
    @mouseup="stopRecording"
    @touchstart="startRecording"
    @touchend="stopRecording"
    @touchcancel="stopRecording"
  >
    <div class="recorder-icon">
      <span v-if="isRecording">STOP</span>
      <span v-else>START</span>
    </div>
  </div>
</template>

<script>
import ElementMixin from './ElementMixin'

const supportedTypes = [
  'video/x-msvideo',
  'video/ogg',
  'video/mpeg',
  'video/webm'
]

export default {
  name: 'VueRecordVideo',
  mixins: [ElementMixin],
  props: {
    mimeType: {
      type: String,
      default: 'video/webm',
      validator: v => supportedTypes.includes(v)
    },
    audio: {
      type: Boolean,
      default: true
    },
    mode: {
      default: 'press'
    }
  },
  computed: {
    constraints () {
      return {
        video: true,
        audio: this.audio
      }
    }
  }
}
</script>