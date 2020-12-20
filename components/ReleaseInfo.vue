<template>
  <div class="artist-info mb-3">
    <h3 class="heading mb-3">
      Our Debut EP Release
    </h3>
    <div>
      <ul class="list-separators mb-3 text-light pl-0">
        <li v-for="( value, key ) in details" :key="key.id" class="info-line mb-2">
          <div v-if="Array.isArray(value)">
            <h6 class="font-weight-bold text-capitalize d-inline mr-2">
              {{ key }}:
            </h6>
            <ul class="list-inline d-inline">
              <li v-for="item in value" :key="item.id" class="list-inline-item">
                {{ item }}
              </li>
            </ul>
          </div>
          <div v-else-if="typeof value === 'object'">
            <h6 class="font-weight-bold text-capitalize d-inline">
              {{ key }}:
            </h6>
            <ul class="list-unstyled">
              <li v-for="(role, name) in value" :key="name.id">
                {{ name }} - <span class="font-italic">{{ role }}</span>
              </li>
            </ul>
          </div>
          <div v-else>
            <h6 class="font-weight-bold text-capitalize d-inline mr-2">
              {{ key }}:
            </h6>
            <!-- eslint-disable-next-line vue/no-v-html -->
            <span v-html="value">{{ value }}</span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      details: {
        inspiration:
          "<p>Goofball has released the first of an installment of EP's they will release known as the 'hits' from the band.  This first EP features three tracks that are sure to rock your face off.</p><p>Each new installment will feature tracks all recorded live at Turbo Snail Studios in Denver.</p><p>Expect two more EP's this year coming from the prolific goof rock band!</p>",
        'release Date': {
          'Now That\'s What I Call Goofball Bucket Vol. 1': 'December 8th 2020'
        },
        // 'Album Release Show': '<br>May 29th @ Roxy on Broadway'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.info-line {
  list-style: none;
}
</style>
