<template>
  <b-img-lazy
    thumbnail
    class="profile-image"
    :alt="altText"
    :src="image"
    @error.native="brokenProfileImage"
  />
</template>

<script>
// This component should be imported, rather than using async require.  This is because async requires result in more
// Vue DOM patching overall, and this component is used in places like chat where it appears many times.  Testing shows
// this has a significant performance benefit.
export default {
  name: 'GroupProfileImage',
  props: {
    image: {
      type: String,
      required: false,
      default: ''
    },
    altText: {
      type: String,
      required: false,
      default: 'Profile picture'
    },
    isThumbnail: {
      type: Boolean,
      required: false
    },
    isModerator: {
      type: Boolean,
      required: false
    }
  },
  methods: {
    brokenProfileImage(event) {
      event.target.src = '/static/defaultprofile.png'
    }
  }
}
</script>

<style scoped lang="scss">
.profile-image {
  width: 100px;
  height: 100px;
}
</style>
