<template>
  <div class="artist-info mb-3">
    <h3 class="heading mb-3">
      Band Info
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
            <ul class="list-unstyled ml-2">
              <li v-for="(role, name) in value" :key="name.id">
                {{ name }} - <span class="badge">{{ role }}</span>
              </li>
            </ul>
          </div>
          <div v-else>
            <h6 class="font-weight-bold text-capitalize d-inline mr-2">
              {{ key }}:
            </h6>{{ value }}
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
        genre: 'Psych Rock',
        hometown: 'Denver',
        members: {
          'Jackson Kaufman': 'Guitar & Vocals',
          'Pieter Montoulieu': 'Guitar & Vocals',
          'Kevin Gy': 'Bass',
          'Steven Sanchez': 'Drums & Vocals',
          'Dalton Groves': 'Keys'
        },
        influences: ['Ween', 'Frank Zappa', 'Mr. Bungle', 'Pink Floyd']
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
