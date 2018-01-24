<template>
  <div>
    <h1>Results for {{$route.params.id}}</h1>

    <div v-if="albumsExists">
      <div v-for="(album, index) in albums" v-bind:key="index">
        <Card
          :title="album.collectionCensoredName"
          :image="album.artworkUrl100"
          :artistName="album.artistName"
          :url="album.artistViewUrl"
          :color="picker(index)"
        />
      </div>
    </div>

    <div v-else>
      <h1>Could Not Find Albums</h1>
    </div>

  </div>
</template>

<script>
import Card from '~/components/Card'
export default {
  middleware: 'search',
  components: {
    Card
  },
  methods: {
    picker(index) {
      return index % 2 == 0 ? 'cyan darken-2' : 'blue'
    }
  },
  computed: {
    albumsExists() {
      return this.$store.state.albums.length > 0
    },
    albums() {
      return this.$store.state.albums
    }
  }

}
</script>
