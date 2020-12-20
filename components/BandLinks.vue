<template>
  <div class="band-links">
    <b-row>
      <b-col class="mb-3">
        <h6 class="font-weight-bold text-capitalize d-inline mr-2">
          Social:
        </h6>
        <ul class="list-inline d-inline">
          <li
            v-for="(link, site) in social"
            :key="link.id"
            class="list-inline-item"
          >
            <a :href="link" target="_blank">{{ site }}</a>
          </li>
        </ul>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h6 class="font-weight-bold text-capitalize d-inline mr-2">
          Music:
        </h6>
        <ul class="list-inline d-inline">
          <li
            v-for="(link, site) in music"
            :key="link.id"
            class="list-inline-item"
          >
            <a :href="link" target="_blank">{{ site }}</a>
          </li>
        </ul>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      social: {
        Facebook: 'https://www.facebook.com/goofballbucket',
        Instagram: 'https://www.instagram.com/goofballbucket/'
      },
      music: {
        Bandcamp: 'https://goofballbucket.bandcamp.com/',
        Spotify: 'https://open.spotify.com/artist/52AB3dcVboSzPFCERW19PI?si=zpXNcIAYR6u9ksnuKGTg4w',
        'Apple Music': 'https://music.apple.com/us/artist/goofball-bucket/1543205594'
      }
    }
  }
}
</script>

<style>
</style>
