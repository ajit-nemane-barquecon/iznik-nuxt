<template>
  <div>
    <b-row v-if="stats" class="m-0">
      <b-col cols="0" md="3" class="d-none d-md-block" />
      <b-col v-if="authority" cols="12" md="6" class="p-0">
        <div class="title pl-2">
          <b-img thumbnail src="/icon.png" class="titlelogo float-right" />
          <span class="head">
            {{ authority.name }}
          </span>
          <div class="d-inline-block align-top pt-2">
            <date-picker
              id="startDate"
              v-model="startDate"
              class="ml-1"
              lang="en"
              type="date"
              append-to-body
              format="YYYY-MM"
              placeholder=""
            />
            <b>-</b>
            <date-picker
              id="endDate"
              v-model="endDate"
              class=""
              lang="en"
              type="date"
              append-to-body
              format="YYYY-MM"
              placeholder=""
            />
            <span class="clickme" @click="reloadData">
              <v-icon name="sync" />
            </span>
          </div>
          <br>
          <v-icon name="globe-europe" /> www.iLoveFreegle.org  <v-icon name="brands/twitter" /> @thisisfreegle  <v-icon name="brands/facebook" /> facebook.com/Freegle
        </div>
        <GmapMap
          ref="gmap"
          :center="{lat:53.9450, lng:-2.5209}"
          :zoom="5"
          :style="'width: ' + mapWidth + '; height: ' + mapWidth + 'px'"
          :options="{
            zoomControl: true,
            mapTypeControl: false,
            scaleControl: false,
            streetViewControl: false,
            rotateControl: false,
            fullscreenControl: true,
            disableDefaultUi: false,
            gestureHandling: 'greedy'
          }"
          @idle="mapIdle"
        >
          <GmapMarker
            v-for="(m, index) in markers"
            :key="index"
            :position="m"
            :clickable="false"
            :draggable="false"
            icon="/mapmarker.gif"
          />
        </GmapMap>
        <b-card variant="white" class="border-white" no-body>
          <b-card-body class="pb-0">
            <b-row class="p-0">
              <b-col class="text-center">
                <v-icon name="balance-scale-left" class="gold titleicon" scale="3" />
                <h5 class="gold">
                  {{ totalWeight.toLocaleString() }}
                  <br>
                  TONNES
                  <br>
                  <span class="text-muted small">
                    {{ range }}
                  </span>
                </h5>
              </b-col>
              <b-col class="text-center">
                <v-icon name="calculator" class="gold titleicon" scale="3" />
                <h5 class="gold">
                  £{{ totalBenefit.toLocaleString() }}
                  <br>
                  BENEFIT
                  <br>
                  <span class="text-muted small">
                    {{ range }}
                  </span>
                </h5>
              </b-col>
              <b-col class="text-center">
                <v-icon name="cloud" class="gold titleicon" scale="3" />
                <h5 class="gold">
                  {{ totalCO2.toLocaleString() }}
                  <br>
                  TONNES CO2
                  <br>
                  <span class="text-muted small">
                    {{ range }}
                  </span>
                </h5>
              </b-col>
              <b-col class="text-center">
                <v-icon name="gift" class="purple titleicon" scale="3" />
                <h5 class="purple">
                  {{ totalGifts.toLocaleString() }}
                  <br>
                  {{ totalGifts | pluralize(['GIFT', 'GIFTS'], { includeNumber: false }) }}
                  <br>
                  <span class="text-muted small">
                    {{ range }}
                  </span>
                </h5>
              </b-col>
              <b-col class="text-center">
                <v-icon name="users" class="text-primary titleicon" scale="3" />
                <h5 class="text-primary">
                  {{ totalMembers.toLocaleString() }}
                  <br>
                  {{ totalMembers | pluralize(['MEMBER', 'MEMBERS'], { includeNumber: false }) }}
                  <br>
                  <span class="text-muted small">
                    {{ end }}
                  </span>
                </h5>
              </b-col>
              <b-col class="text-center">
                <v-icon name="map-marker-alt" class="green titleicon" scale="3" />
                <h5 class="green">
                  {{ groupcount.toLocaleString() }}
                  <br>
                  {{ groupcount | pluralize(['COMMUNITY', 'COMMUNITIES'], { includeNumber: false }) }}
                  <br>
                  <span class="text-muted small">
                    {{ groupcount | pluralize(['SERVES', 'SERVE'], { includeNumber: false }) }} THIS AREA
                  </span>
                </h5>
              </b-col>
            </b-row>
          </b-card-body>
        </b-card>
        <b-row class="m-0 border border-light">
          <b-col class="bg-white text-faded">
            <div class="iconlist">
              <v-icon name="glass-martini" />
              <v-icon name="camera" />
              <v-icon name="print" />
              <v-icon name="binoculars" />
              <v-icon name="umbrella" />
              <v-icon name="coffee" />
              <v-icon name="bath" />
              <v-icon name="clock" />
              <v-icon name="bicycle" />
              <v-icon name="hat-wizard" />
              <v-icon name="bed" />
              <v-icon name="laptop" />
              <v-icon name="gift" />
              <v-icon name="utensils" />
              <v-icon name="tablet-alt" />
              <v-icon name="crown" />
              <v-icon name="baby-carriage" />
              <v-icon name="headphones" />
              <v-icon name="tv" />
              <v-icon name="car" />
              <v-icon name="socks" />
              <v-icon name="mobile-alt" />
              <v-icon name="glass-martini" />
              <v-icon name="camera" />
              <v-icon name="print" />
              <v-icon name="binoculars" />
              <v-icon name="umbrella" />
              <v-icon name="coffee" />
              <v-icon name="bath" />
              <v-icon name="clock" />
              <v-icon name="bicycle" />
              <v-icon name="hat-wizard" />
              <v-icon name="bed" />
              <v-icon name="laptop" />
              <v-icon name="gift" />
              <v-icon name="utensils" />
              <v-icon name="tablet-alt" />
              <v-icon name="crown" />
              <v-icon name="baby-carriage" />
              <v-icon name="headphones" />
              <v-icon name="tv" />
              <v-icon name="car" />
              <v-icon name="socks" />
              <v-icon name="mobile-alt" />
              <v-icon name="glass-martini" />
              <v-icon name="camera" />
              <v-icon name="print" />
              <v-icon name="binoculars" />
              <v-icon name="umbrella" />
              <v-icon name="coffee" />
              <v-icon name="bath" />
              <v-icon name="clock" />
              <v-icon name="bicycle" />
              <v-icon name="hat-wizard" />
              <v-icon name="bed" />
              <v-icon name="laptop" />
              <v-icon name="gift" />
              <v-icon name="utensils" />
              <v-icon name="tablet-alt" />
              <v-icon name="crown" />
              <v-icon name="baby-carriage" />
              <v-icon name="headphones" />
              <v-icon name="tv" />
              <v-icon name="car" />
              <v-icon name="socks" />
              <v-icon name="mobile-alt" />
              <v-icon name="glass-martini" />
              <v-icon name="camera" />
              <v-icon name="print" />
              <v-icon name="binoculars" />
              <v-icon name="umbrella" />
              <v-icon name="coffee" />
              <v-icon name="bath" />
              <v-icon name="clock" />
              <v-icon name="bicycle" />
              <v-icon name="hat-wizard" />
              <v-icon name="bed" />
              <v-icon name="laptop" />
              <v-icon name="gift" />
              <v-icon name="utensils" />
              <v-icon name="tablet-alt" />
              <v-icon name="crown" />
              <v-icon name="baby-carriage" />
              <v-icon name="headphones" />
              <v-icon name="tv" />
              <v-icon name="car" />
              <v-icon name="socks" />
              <v-icon name="mobile-alt" />
            </div>
          </b-col>
        </b-row>
        <b-row class="m-0">
          <b-col class="border border-white p-0 bg-white text-center pt-1">
            <H5>WEIGHTS (KG)</H5>
          </b-col>
          <b-col class="border border-white p-0 bg-white text-center pt-1">
            <H5>MEMBERS</H5>
          </b-col>
        </b-row>
        <b-row class="m-0">
          <b-col class="border border-white p-0 bg-white overflow-hidden">
            <GChart
              type="ColumnChart"
              :data="weightData"
              :options="weightOptions"
            />
          </b-col>
          <b-col class="border border-white p-0 bg-white overflow-hidden">
            <GChart
              type="LineChart"
              :data="memberData"
              :options="memberOptions"
            />
          </b-col>
        </b-row>
        <b-card variant="white" class="border-white">
          <b-card-text>
            <h2 class="text-center">
              Freegle Communities serving {{ authority.name }}
            </h2>
            <b-table striped :items="items" :fields="fields">
              <template v-slot:cell(members)="data">
                <!-- eslint-disable-next-line -->
                <span v-html="data.value" />
              </template>
              <template v-slot:cell(monthly)="data">
                <!-- eslint-disable-next-line -->
                <span v-html="data.value" />
              </template>
            </b-table>
            <p v-if="someoverlap" class="text-muted small pl-1 mb-0">
              * The area for this Freegle community partly overlaps the area you're looking at, so we've added an appropriate percentage.
            </p>
          </b-card-text>
        </b-card>
        <b-row class="m-0">
          <b-col class="p-0">
            <div class="title pl-2">
              <b-img thumbnail src="/icon.png" class="titlelogo float-right" />
              <span class="head">
                {{ totalWeight }} TONNES REUSED
              </span>
              <br>
              <span class="small">
                {{ range }}
              </span>
            </div>
          </b-col>
        </b-row>
      </b-col>
    </b-row>
    <b-row v-else>
      <b-col class="text-center">
        <h4>Crunching the numbers...</h4>
        <p>This may take a minute.</p>
        <b-img-lazy src="~/static/loader.gif" alt="Loading" />
      </b-col>
    </b-row>
  </div>
</template>

<script>
// There are a bunch of icons we need only on this page.  By requiring them here we avoid
// requiring them in the vue-awesome plugin.  That makes them available everywhere - but
// increases the bundle size.  Putting them here allows better bundling.
import { GChart } from 'vue-google-charts'
import Wkt from 'wicket'
import 'wicket/wicket-gmap3'
import { gmapApi } from 'vue2-google-maps'
import { TablePlugin } from 'bootstrap-vue'
import Vue from 'vue'
import DatePicker from 'vue2-datepicker'
import 'vue2-datepicker/index.css'
import loginOptional from '@/mixins/loginOptional.js'
import buildHead from '@/mixins/buildHead.js'

Vue.use(TablePlugin)

export default {
  layout: 'empty',
  components: {
    GChart,
    DatePicker
  },
  mixins: [loginOptional, buildHead],
  data() {
    return {
      startDate: null,
      endDate: null,
      authority: null,
      stats: null,
      groupcount: null,
      // No animations as we want the SSR to return the whole thing.
      weightOptions: {
        interpolateNulls: false,
        legend: { position: 'none' },
        chartArea: { width: '80%', height: '80%' },
        bar: { groupWidth: '98%' },
        vAxis: { viewWindow: { min: 0 } },
        hAxis: {
          format: 'MMM yyyy'
        },
        series: {
          0: { color: 'green' }
        }
      },
      memberOptions: {
        interpolateNulls: false,
        legend: { position: 'none' },
        chartArea: { width: '80%', height: '80%' },
        vAxis: { viewWindow: { min: 0 } },
        hAxis: {
          format: 'MMM yyyy'
        },
        series: {
          0: { color: 'blue' }
        }
      },
      fields: [
        {
          key: 'location',
          label: 'Community Location'
        },
        {
          key: 'members',
          label: 'Membership'
        },
        {
          key: 'monthly',
          label: 'Average Kgs Reused Monthly'
        }
      ],
      addedPolygons: false
    }
  },
  computed: {
    google: {
      get() {
        return process.browser ? gmapApi : []
      }
    },
    mapHeight() {
      const contWidth = this.$refs.mapcont ? this.$refs.mapcont.$el.width : 0
      return contWidth
    },
    mapWidth() {
      let height = 0

      if (process.browser) {
        height = Math.floor(window.innerHeight / 2)
        height = height < 200 ? 200 : height
      }

      return height
    },
    totalWeight() {
      let total = 0

      for (const groupid in this.stats) {
        const overlap = this.overlap(groupid)
        const stat = this.stats[groupid]
        for (const w of stat.Weights) {
          total += w.count * overlap
        }
      }

      return Math.round(total / 100) / 10
    },
    // Benefit of reuse per tonne is £711 and CO2 impact is -0.51tCO2eq based on WRAP figures.
    // http://www.wrap.org.uk/content/monitoring-tools-and-resources
    totalBenefit() {
      return Math.round(this.totalWeight * 711)
    },
    totalCO2() {
      return Math.round(this.totalWeight * 0.51 * 10000) / 10000
    },
    totalGifts() {
      let count = 0

      for (const groupid in this.stats) {
        const overlap = this.overlap(groupid)
        const stat = this.stats[groupid]
        const outcomes = stat.OutcomesPerMonth

        const start = this.$dayjs(this.startDate)
        const end = this.$dayjs(this.endDate)

        for (const outcome of outcomes) {
          const m = this.$dayjs(outcome.date + '-01')

          if (!m.isBefore(start) && !m.isAfter(end)) {
            count += outcome.count * overlap
          }
        }
      }

      return Math.round(count)
    },
    weightData() {
      const bymonth = []

      for (const groupid in this.stats) {
        const overlap = this.overlap(groupid)
        const stat = this.stats[groupid]
        const weight = stat.Weights

        for (const a of weight) {
          const mon = a.date.substring(0, 7)

          if (!bymonth[mon]) {
            bymonth[mon] = 0
          }

          bymonth[mon] += a.count * overlap
        }
      }

      const ret = [['Date', 'Count']]
      for (const mon in bymonth) {
        ret.push([new Date(mon + '-01'), bymonth[mon]])
      }

      return ret
    },
    memberData() {
      const ret = [['Date', 'Count']]
      const dates = []

      for (const groupid in this.stats) {
        const overlap = this.overlap(groupid)
        const stat = this.stats[groupid]
        const members = stat.ApprovedMemberCount

        if (members) {
          for (const a of members) {
            if (!dates[a.date]) {
              dates[a.date] = 0
            }

            dates[a.date] += parseInt(a.count) * overlap
          }
        }
      }

      for (const date in dates) {
        ret.push([new Date(date), Math.round(dates[date])])
      }

      return ret
    },
    totalMembers() {
      let ret = 0
      const data = this.memberData
      if (data) {
        const last = data.pop()
        ret = last[1]
      }
      return ret
    },
    range() {
      const start = this.$dayjs(this.startDate)
        .format('MMM YY')
        .toUpperCase()
      const end = this.$dayjs(this.endDate)
        .format('MMM YY')
        .toUpperCase()
      return start + ' - ' + end
    },
    monthsCovered() {
      const ret = this.$dayjs(this.endDate).diff(
        this.$dayjs(this.startDate),
        'months'
      )
      console.log('Months covered', this.startDate, this.endDate, ret)
      return ret + 1
    },
    end() {
      const end = this.$dayjs(this.endDate)
        .format('MMM YY')
        .toUpperCase()
      return end
    },
    someoverlap() {
      const groups = Object.values(this.stats)
      let someoverlaps = false

      for (const ix in groups) {
        const group = groups[ix]
        if (group.overlap < 1) {
          someoverlaps = true
        }
      }

      return someoverlaps
    },
    items() {
      const groups = Object.values(this.stats)
      groups.sort(function(a, b) {
        return b.avpermonth - a.avpermonth
      })

      const ret = []

      for (const ix in groups) {
        const group = groups[ix]

        if (group.ApprovedMemberCount.length > 0) {
          ret.push({
            location: group.group.namedisplay + (group.overlap < 1 ? ' *' : ''),
            members:
              Math.round(
                group.ApprovedMemberCount[group.ApprovedMemberCount.length - 1]
                  .count * group.overlap
              ).toLocaleString() +
              (group.overlap < 1
                ? ' (<span class="text-muted small">of ' +
                  Math.round(
                    group.ApprovedMemberCount[
                      group.ApprovedMemberCount.length - 1
                    ].count
                  ).toLocaleString() +
                  ')</span>'
                : ''),
            monthly:
              Math.round(group.avpermonth) +
              (group.overlap < 1
                ? ' (<span class="text-muted small">of ' +
                  Math.round(group.totalweight) +
                  ')</span>'
                : '')
          })
        }
      }

      return ret
    },
    markers() {
      const google = gmapApi()
      const ret = []

      if (google) {
        for (const groupid in this.stats) {
          const marker = new google.maps.LatLng(
            this.stats[groupid].group.lat,
            this.stats[groupid].group.lng
          )
          ret.push(marker)
        }
      }

      return ret
    }
  },
  created() {
    this.id = this.$route.params.id

    // Default end is last complete month, and start is a year before that, so we cover twelve months.
    this.endDate = this.$dayjs()
      .subtract(1, 'month')
      .endOf('month')
      .format()
    this.startDate = this.$dayjs(this.endDate)
      .subtract(1, 'year')
      .add(1, 'month')
      .startOf('month')
      .format()
  },
  mounted() {
    this.fetchData(this.$store, this.id)
  },
  methods: {
    async fetchData(store, id) {
      await store.dispatch('authorities/fetch', {
        id: id
      })

      let groupcount = 0
      const stats = []

      const authority = store.getters['authorities/get'](id)
      const start = this.$dayjs(this.startDate).format('YYYY-MM-DD')
      const end = this.$dayjs(this.endDate).format('YYYY-MM-DD')

      for (const group of authority.groups) {
        await store.dispatch('stats/clear')
        await store.dispatch('stats/fetch', {
          group: group.id,
          grouptype: 'Freegle',
          start: start,
          end: end
        })

        // Check if the group has a significant overlap. No point cluttering things up with groups which don't really
        // contribute.
        const overlap = group.overlap
        const weights = store.getters['stats/get']('Weight')

        let totalWeight = 0
        for (const w of weights) {
          totalWeight += w.count * overlap
        }

        const avpermonth = totalWeight / this.monthsCovered

        // If there is only one group in the area we're looking at, or the group is entirely contained within the
        // area, then show it irrespective of activity otherwise it looks silly.
        if (avpermonth > 1 || authority.groups.length === 1 || overlap === 1) {
          groupcount++

          stats[group.id] = {
            overlap: overlap,
            avpermonth: avpermonth,
            totalweight: totalWeight,
            Weights: weights,
            ApprovedMemberCount: store.getters['stats/get'](
              'ApprovedMemberCount'
            ),
            OutcomesPerMonth: store.getters['stats/get']('OutcomesPerMonth'),
            group: group
          }
        }
      }

      this.authority = authority
      this.stats = stats
      this.groupcount = groupcount
    },
    overlap: function(groupid) {
      for (const group of this.authority.groups) {
        if (parseInt(group.id) === parseInt(groupid)) {
          return group.overlap
        }
      }

      return 0
    },
    mapPoly: function(poly, options) {
      const google = gmapApi()
      let bounds = null
      const wkt = new Wkt.Wkt()
      wkt.read(poly)

      const mapobj = this.$refs.gmap.$mapObject
      const obj = wkt.toObject(mapobj.defaults)

      if (obj) {
        // This might be a multipolygon.
        bounds = new google.maps.LatLngBounds()

        if (Array.isArray(obj)) {
          for (const ent of obj) {
            ent.setMap(mapobj)
            ent.setOptions(options)
            const thisbounds = ent.getBounds()
            bounds.extend(thisbounds.getNorthEast())
            bounds.extend(thisbounds.getSouthWest())
          }
        } else {
          obj.setMap(mapobj)
          obj.setOptions(options)
          bounds = obj.getBounds()
        }
      }

      return bounds
    },
    mapIdle() {
      if (!this.addedPolygons) {
        const google = gmapApi()
        this.addedPolygons = true

        // No getBounds on polygon by default.
        google.maps.Polygon.prototype.getBounds = function() {
          const bounds = new google.maps.LatLngBounds()
          const paths = this.getPaths()
          let path
          for (let i = 0; i < paths.getLength(); i++) {
            path = paths.getAt(i)
            for (let ii = 0; ii < path.getLength(); ii++) {
              bounds.extend(path.getAt(ii))
            }
          }
          return bounds
        }

        const bounds = this.mapPoly(this.authority.polygon, {
          fillColor: 'blue',
          strokeWeight: 0,
          fillOpacity: 0.2
        })

        this.$refs.gmap.$mapObject.fitBounds(bounds)

        for (const groupid in this.stats) {
          const polygon = this.stats[groupid].group.poly

          this.mapPoly(polygon, {
            fillColor: 'grey',
            strokeWeight: 0,
            fillOpacity: 0.2
          })
        }
      }
    },
    reloadData() {
      if (
        this.startDate &&
        this.endDate &&
        this.$dayjs(this.endDate).isAfter(this.$dayjs(this.startDate))
      ) {
        this.stats = null
        this.fetchData(this.$store, this.id)
      }
    }
  },
  head() {
    return this.buildHead('Statistics', 'See stats and graphs for Freegle')
  }
}
</script>

<style scoped lang="scss">
@import 'color-vars';

.title {
  background-color: $color-green--darker;
  color: $color-white !important;
}

.titlelogo {
  width: 72px;
}

.titleicon {
  width: 2rem;
  height: 2rem;
}

.head {
  font-size: 2rem;
}

.purple {
  color: $color-purple !important;
}

.gold {
  color: $color-gold !important;
}

.green {
  color: $color-green--darker !important;
}

.iconlist {
  white-space: nowrap;
  overflow-x: hidden;
}

::v-deep .mx-datepicker {
  width: 100px;
}
</style>
