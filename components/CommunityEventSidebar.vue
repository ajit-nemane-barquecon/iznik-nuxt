<template>
  <div>
    <b-card v-if="events.length" variant="white" no-body>
      <b-card-body class="p-0">
        <b-btn variant="white" class="float-right m-1" @click="showEventModal">
          <v-icon name="plus" /> Add
        </b-btn>
        <nuxt-link to="/communityevents">
          <h4 class="pl-1 pt-1">
            <v-icon name="calendar-alt" scale="2" /> Community Events
          </h4>
        </nuxt-link>
        <p class="text-center small">
          These are local events, posted by other freeglers like you.
        </p>
        <div v-for="event in events" :key="'event-' + event.id" class="">
          <CommunityEvent v-if="!event.pending" :summary="true" :event="event" />
        </div>
      </b-card-body>
    </b-card>
    <CommunityEventModal ref="eventmodal" :start-edit="true" />
  </div>
</template>
<script>
import CommunityEvent from './CommunityEvent'
const CommunityEventModal = () => import('~/components/CommunityEventModal')

export default {
  components: {
    CommunityEvent,
    CommunityEventModal
  },
  data: function() {
    return {}
  },
  computed: {
    events() {
      return this.$store.getters['communityevents/sortedList']
    }
  },
  mounted() {
    this.$store.dispatch('communityevents/clear')

    // Delay a little bit to give the main pane a chance to load.
    setTimeout(() => {
      this.$store.dispatch('communityevents/fetch')
    }, 1000)
  },
  methods: {
    showEventModal() {
      this.$refs.eventmodal.show()
    }
  }
}
</script>
