<template>
  <div class="container p-0">
    <span @click="rotateLeft">
      <v-icon label="Rotate left" class="topleft clickme" title="Rotate left">
        <v-icon name="circle" scale="2" />
        <v-icon
          name="reply"
          class="image__icon"
        />
      </v-icon>
    </span>
    <span @click="rotateRight">
      <v-icon label="Rotate right" class="topright clickme" title="Rotate right" flip="horizontal">
        <v-icon name="circle" scale="2" />
        <v-icon
          name="reply"
          class="image__icon"
        />
      </v-icon>
    </span>
    <span @click="remove">
      <v-icon label="Remove this photo" class="bottomright clickme" title="Remove this photo">
        <v-icon name="circle" scale="2" />
        <v-icon
          name="trash-alt"
          class="image__icon"
        />
      </v-icon>
    </span>
    <b-img lazy :src="paththumb + '?' + cacheBust" rounded thumbnail class="imagepreview" />
  </div>
</template>

<style scoped lang="scss">
@import 'color-vars';

.imagepreview {
  width: 150px;
}

.bottomright {
  bottom: 12px;
  right: 10px;
  position: absolute;
}

.topleft {
  top: 12px;
  left: 10px;
  position: absolute;
}

.topright {
  top: 12px;
  right: 10px;
  position: absolute;
}

.container {
  position: relative;
}

.image__icon {
  color: $color-white;
}
</style>

<script>
export default {
  props: {
    id: {
      type: Number,
      required: true
    },
    path: {
      type: String,
      required: true
    },
    paththumb: {
      type: String,
      required: true
    }
  },
  data: function() {
    return {
      cacheBust: Date.now()
    }
  },
  methods: {
    remove() {
      this.$emit('remove', this.id)
    },
    rotate(deg) {
      this.$axios
        .post(process.env.API + '/image', {
          id: this.id,
          rotate: deg,
          bust: Date.now()
        })
        .then(() => {
          this.cacheBust = Date.now()
        })
    },
    rotateLeft() {
      this.rotate(90)
    },
    rotateRight() {
      this.rotate(-90)
    }
  }
}
</script>
