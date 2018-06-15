<template>
  <div>
    <v-layout>
      <v-flex xs6>
        <panel title="Song Info">
          <v-layout>
            <v-flex xs6>
              <div class="song-title">
                {{song.title}}
              </div>
              <div class="song-artist">
                {{song.artist}}
              </div>
              <div class="song-genre">
                {{song.genre}}
              </div>
            </v-flex>

            <v-flex xs6>
              <img class="album-image"
              v-bind:src="song.albumImageUrl">
              <br>
              {{song.album}}
            </v-flex>
          </v-layout>
        </panel>
      </v-flex>
      <v-flex xs6>
        <panel title="Video" class="ml-2">
          <youtube
            :video-id="youtubeId"
            :player-width="350"
            :player-height="200"></youtube>
        </panel>
      </v-flex>
      </v-layout>
      <v-layout class="mt-2">
        <v-flex xs6>
          <panel title="Tabs">
            <textarea
              readonly
              v-model="song.tab">
            </textarea>
          </panel>
        </v-flex>
        <v-flex xs6>
          <panel title="Lyrics" class="ml-2">
            <textarea
              readonly
              v-model="song.lyrics">
            </textarea>
          </panel>
        </v-flex>
    </v-layout>
  </div>
</template>

<script>
import SongsService from '@/services/SongsService'
import Panel from '@/components/Panel'
export default {
  components: {
    Panel
  },
  data () {
    return {
      song: {}
    }
  },
  async mounted () {
    const songId = this.$store.state.route.params.songId
    this.song = (await SongsService.show(songId)).data
  }
}
</script>

<style>
.song{
  padding: 20px;
  height: 330px;
  overflow: hidden;
}
.song-title{
  font-size: 24px;
}
.song-artist{
  font-size: 24px;
}
.song-genre{
  font-size: 20px;
}
.album-image{
  width: 100%;
  margin:0 auto;
}
textarea {
  width: 100%;
  font-family: monospace;
  border: none;
  height: 600px;
  border-style: none;
  border-color:transparent;
  overflow: auto;
  padding: 20px;
}
</style>
