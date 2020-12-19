<template>
  <div class="artist-info mb-3">
    <h3 class="heading mb-3">
      Our Second Full Length Album
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
          "<p>Based on the run down, dumpy looking motel off of Sheridan and 1st Avenue in Lakewood, \"Emily's Aparments\" is a concept album that revolves around what kind of characters, events and oddities you might find there.</p><p>Completely written, recorded, and produced over the last 2 years by Pieter and Jackson, this album takes you through a vast musical landscape of prog-rock to soul, groove to grunge, psychedelic to brutal and much more.</p><p>Each of the 17 songs, written for each of the 17 rooms for rent at Emily's, draws from a different musical influence from the dudes so that no two songs sound the same, which the band agrees they couldn't live without.</p>",
        'release Dates': {
          // 'Queen of Farts': 'April 8th',
          // 'Les Do It': 'April 22nd',
          // 'Hammy Mac': 'May 6th',
          // Jankfest: 'May 20th',
          'Full Album': 'May 26th'
        },
        'Album Release Show': '<br>May 29th @ Roxy on Broadway'
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
