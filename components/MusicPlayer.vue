<template>
  <div class="music-player mb-4">
    <h3 class="mb-3">
      Music
    </h3>
    <b-card
      v-if="tracksLoaded"
      class="player"
      no-body
    >
      <div slot="header">
        <b-row>
          <b-col>
            <b-button-group>
              <b-button @click="togglePlayButton(index)">
                <ios-play-icon v-show="!playing" /><ios-pause-icon v-show="playing" />
              </b-button>
              <b-button @click="skip('prev')">
                <ios-skip-backward-icon />
              </b-button>
              <b-button @click="skip('next')">
                <ios-skip-forward-icon />
              </b-button>
            </b-button-group>
          </b-col>
          <b-col class="control-volume d-flex align-items-center text-light">
            <ios-volume-low-icon class="mr-2" />
            <b-form-input v-model="volume" type="range" max="1" step="0.1" @input="updateVolume(volume)" />
            <ios-volume-high-icon class="ml-2" />
          </b-col>
        </b-row>
      </div>
      <b-list-group flush>
        <b-list-group-item
          v-for="(track, index) in playlist"
          v-show="track.display"
          :key="track.title"
          class="d-flex"
          :class="[{selected: track === selectedTrack}]"
          variant="dark"
          button
          @click="selectTrack(track, index)"
        >
          {{ formatTrackNumber(index) }} {{ track.title }}
          <span class="ml-auto">{{ formatMinutes(track.howl.duration()) }}</span>
        </b-list-group-item>
      </b-list-group>

      <b-card-body class="text-light">
        <p
          v-if="this.selectedTrack"
          class="mb-0"
        >
          {{ this.selectedTrack.description }}
        </p>
      </b-card-body>
    </b-card>
  </div>
</template>

<script>
require('vue-ionicons/ionicons.css')
import IosPlayIcon from 'vue-ionicons/dist/ios-play.vue'
import IosPauseIcon from 'vue-ionicons/dist/ios-pause.vue'
import IosSkipBackwardIcon from 'vue-ionicons/dist/ios-skip-backward.vue'
import IosSkipForwardIcon from 'vue-ionicons/dist/ios-skip-forward.vue'
import IosVolumeLowIcon from 'vue-ionicons/dist/ios-volume-low.vue'
import IosVolumeHighIcon from 'vue-ionicons/dist/ios-volume-high.vue'

/* eslint-disable */
import { Howl, Howler } from 'howler'

export default {
  components: {
    IosPlayIcon,
    IosPauseIcon,
    IosSkipBackwardIcon,
    IosSkipForwardIcon,
    IosVolumeLowIcon,
    IosVolumeHighIcon
  },
  data() {
    return {
      volume: 0.8,
      selectedTrack: null,
      index: 0,
      playing: false,
      loop: false,
      shuffle: false,
      seek: 0,
      tracksLoaded: false,
      playlist: [
        {
          title: 'Queen of Farts',
          artist: 'shwarma',
          description: 'The first single from Emily\'s Aparments.  This song takes influence from queen and the talking heads.',
          howl: null,
          display: true
        },
        {
          title: 'Les Do It',
          artist: 'shwarma',
          description: 'Second Emily\'s single. This grimy track draws influence from Primus mostly, but also the Claypool-Lennon Delerium.',
          howl: null,
          display: true
        },
        {
          title: 'Hammy Mac',
          artist: 'shwarma',
          description: 'This is the third single from Emily\'s.  The tape machines slowed tempo and pitch affect make it seem like a heavy blanket is draped over the back of your eyes.  This one might give you the munchies.',
          howl: null,
          display: true
        },
        {
          title: 'Jankfest',
          artist: 'shwarma',
          description: 'The fourth single off the new album.  Jankfest is about a really janky and shitty music festival hosted in the lot behind the motel.  Debauchery and madness happen here regularily.',
          howl: null,
          display: true
        },
        {
          title: 'Eel Fingers',
          artist: 'shwarma',
          description: 'This was the featured single off the briny deep, shwarma\'s first full length.  It also was the featured track for their music video they produced themselves.  Check it out on their YouTube channel.',
          howl: null,
          display: true
        },
        {
          title: 'Farts of Palm',
          artist: 'shwarma',
          description: 'This one starts with your toes in the sand and a marg in hand, and ends with a fiery guitar lead leaving shred-trails in the sky.',
          howl: null,
          display: true
        },
        {
          title: 'Drug of Choice',
          artist: 'shwarma',
          description: 'This funky number was influenced by the likes of T Rex mostly.  The boyos had a blast recording a Zappa inspired vocal reversal trick at the end of this one.',
          howl: null,
          display: true
        },
        {
          title: 'Siquor',
          artist: 'shwarma',
          description: 'This sappy love song hates your alcoholic ex, but it\'s soulful delivery draws inspirato from Al Green and The Temptations',
          howl: null,
          display: true
        },
        {
          title: 'Spaghetti Haus',
          artist: 'shwarma',
          description: 'One of shwarmas first songs ever written.  This middle eastern inspired dish boasts hints of odd time signatures and tastes of not giving a shit.',
          howl: null,
          display: true
        },
        {
          title: 'Moldelo',
          artist: 'shwarma',
          description: 'This latin jam was inspired by a true story.  While filming a green screen series in Pieter\'s basement our friend was accedentally fed an old moldy modelo in front of the camera.  He turned out ok.',
          howl: null,
          display: true
        },
      ]
    }
  },
  computed: {
    currentTrack () {
      return this.playlist[this.index]
    },
    progress () {
      if (this.currentTrack.howl.duration() === 0) return 0
      return this.seek / this.currentTrack.howl.duration()
    },
    getTrackInfo () {
      let artist = this.currentTrack.artist,
          title = this.currentTrack.title,
          seek = this.seek,
          duration = this.currentTrack.howl.duration()
      return {
        artist,
        title,
        seek,
        duration,
      }
    }
  },
  created: function() {
    Howler.volume(this.volume)

    this.playlist.forEach(track => {
      const file = track.title.replace(/\s/g, '_')

      track.howl = new Howl({
        src: [require(`@/assets/playlist/${file}.mp3`)]
      })

      console.log(track.howl)
    })

    console.log(this.tracksLoaded);
    this.tracksLoaded = true
    // self.selectedTrack =
    console.log('Tracks loaded timer')

  },
  methods: {
    togglePlayButton(index){
      if (this.playing) {
        this.pause()
      } else {
        this.play(index)
      }
    },
    formatMinutes(value) {
      if (!value || typeof value !== 'number') {
        return '00:00'
      }

      let min = parseInt(value / 60)
      let sec = parseInt(value % 60)

      min = min < 10 ? '0' + min : min
      sec = sec < 10 ? '0' + sec : sec
      value = min + ':' + sec

      return value
    },
    formatTrackNumber(value) {
      const number = value + 1

      if (number < 10) {
        return '0' + number + '.'
      }

      return number + '.'
    },
    selectTrack (track, index) {
      this.stop()
      this.selectedTrack = track
      this.play(index)
      console.log(this.selectedTrack.description)
    },
    play (index) {
      let selectedTrackIndex = this.playlist.findIndex(track => track === this.selectedTrack)
      if (typeof index === 'number') {
        index = index
      } else if (this.selectedTrack) {
        if (this.selectedTrack != this.currentTrack) {
          this.stop()
        }
        index = selectedTrackIndex
      } else {
        index = this.index
      }
      let track = this.playlist[index].howl
      if (track.playing()) {
        return
      } else {
        track.play()
      }

      this.selectedTrack = this.playlist[index]
      this.playing = true
      this.index = index
    },
    pause () {
      this.currentTrack.howl.pause()
      this.playing = false
    },
    stop () {
      this.currentTrack.howl.stop()
      this.playing = false
    },
    skip (direction) {
      let index = 0,
          lastIndex = this.playlist.length - 1
      if (this.shuffle) {
        index = Math.round(Math.random() * lastIndex)
        while (index === this.index) {
          index = Math.round(Math.random() * lastIndex)
        }
      } else if (direction === "next") {
        index = this.index + 1
        if (index >= this.playlist.length) {
          index = 0
        }
      } else {
        index = this.index - 1
        if (index < 0) {
          index = this.playlist.length - 1
        }
      }
      this.skipTo(index)
    },
    skipTo (index) {
      if (this.currentTrack) {
        this.currentTrack.howl.stop()
      }
      this.play(index)
    },
    toggleLoop (value) {
      this.loop = value
    },
    toggleShuffle (value) {
      this.shuffle = value
    },
    setSeek (percents) {
      let track = this.currentTrack.howl
      if (track.playing()) {
        track.seek((track.duration() / 100) * percents)
      }
    },
    updateVolume (volume) {
      Howler.volume(volume)
    },
  }
}
/* eslint-enable */
</script>

<style lang="scss" scoped>
.selected {
  background-color: #500285 !important;
}

.playlist {
  overflow: auto;
}

.card.player {
  border-color: #500285;

  .card-header,
  .card-body {
    background-color: #24013b;
  }

  .list-group-item {
    background-color: #38005d;
    color: #fedfff;
    transition: background-color 0.2s ease-in-out;
  }
  .btn-group {
    .btn {
      background-color: #500285;
      border-color: #24013b;
      line-height: 1;

      .ion {
        font-size: 1.5rem;
      }

      &:focus,
      &:touch,
      &:hover {
        background-color: #24013b !important;
      }
    }
  }
  .control-volume {
    .ion {
      font-size: 2rem;
    }
  }
}
</style>
