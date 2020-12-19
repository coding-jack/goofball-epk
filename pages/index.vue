<template>
  <div class="container p-5">
    <b-row>
      <b-col class="text-center">
        <the-header />
      </b-col>
    </b-row>
    <b-row class="pt-5">
      <b-col lg="6">
        <img src="~/assets/images/album_cover.jpg" class="img-fluid rounded-lg mb-4">
      </b-col>
      <b-col lg="6">
        <emilys-info />
      </b-col>
    </b-row>
    <b-row class="py-5">
      <b-col lg="6">
        <band-bio />
      </b-col>
      <b-col lg="6">
        <band-camp-embed />
      </b-col>
    </b-row>
    <b-row class="pb-5">
      <b-col lg="6">
        <band-photos />
      </b-col>
      <b-col lg="6">
        <band-info />
        <band-links />
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <the-footer />
      </b-col>
    </b-row>
  </div>
</template>

<script>
import BandBio from '../components/BandBio'
import BandInfo from '../components/BandInfo'
import BandLinks from '../components/BandLinks'
import BandPhotos from '../components/BandPhotos'
// import MusicPlayer from '../components/MusicPlayer'
import TheHeader from '../components/TheHeader'
import TheFooter from '../components/TheFooter'
import EmilysInfo from '../components/EmilysInfo'
import BandCampEmbed from '../components/BandCampEmbed'

export default {
  components: {
    BandBio,
    BandInfo,
    BandLinks,
    BandPhotos,
    // MusicPlayer,
    TheHeader,
    TheFooter,
    EmilysInfo,
    BandCampEmbed
  },
  head() {
    return {
      title: "Emily's Aparments - electronic press kit",
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: 'description',
          name: 'description',
          content:
            'Electronic press kit for Denver psychedelic rock band, shwarma'
        }
      ]
    }
  }
}
</script>
