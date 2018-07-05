<template>
<v-layout>
  <v-flex xs4>
    <panel title="Song Metadata">
      <v-text-field 
            name="title"
            type="text"
            required
            :rules="[rules.required]"
            label="Title"
            v-model="song.title"></v-text-field>

      <v-text-field 
            name="artist"
            type="text"
            required
            :rules="[rules.required]"
            label="Artist"
            v-model="song.artist"></v-text-field>

      <v-text-field 
            name="genre"
            type="text"
            required
            :rules="[rules.required]"
            label="Genre"
            v-model="song.genre"></v-text-field>

      <v-text-field 
            name="album"
            type="text"
            required
            :rules="[rules.required]"
            label="Album"
            v-model="song.album"></v-text-field>
      <v-text-field 
            name="albumImage"
            type="text"
            required
            :rules="[rules.required]"
            label="Album Image"
            v-model="song.albumImage"></v-text-field>

      <v-text-field 
            name="youtubeId"
            type="text"
            required
            :rules="[rules.required]"
            label="Youtube ID"
            v-model="song.youtubeId"></v-text-field>
    </panel>
  </v-flex>
  <v-flex xs8>
    <panel title="Song Structure" class="ml-4">
      <v-text-field 
              name="tab"
              type="text"
              required
              :rules="[rules.required]"
              label="Tab"
              multi-line
              v-model="song.tab"></v-text-field>

      <v-text-field v-model="song.lyrics"
              name="lyrics"
              type="text"
              required
              :rules="[rules.required]"
              label="Lyrics"
              multi-line
              ></v-text-field>
    </panel>
    <div class="danger-alert" v-if="error">
      {{error}}
    </div>
    <v-btn class="red darken-2" dark @click="save">Save Song</v-btn>
  </v-flex>
</v-layout>
</template>
<script>
import Panel from '@/components/Panel'
import SongsService from '@/services/SongsService'
export default {
  data(){
    return{
      song: {
        title :null,
        artist : null,
        genre:null,
        album:null,
        albumImage:null,
        youtubeId:null,
        lyrics:null,
        tab: null
      },
      error:null,
      rules:{
        required:(value) => !!value || 'Required'
      }
    }
  },
  components: {
    Panel
  },
  methods : {
    async save(){
      this.error = null
      const areAllFieldsFilledIn = Object.keys(this.song).every(key=> !!this.song[key])
      if(!areAllFieldsFilledIn){
        this.error = 'Please fill in all the required fields'
        return
      }
      const songId = this.$store.state.route.params.songId

      try {
        await SongsService.put(this.song)
        this.$router.push({name:'song',params:{songId:songId}})
      } catch (error) {
        console.log(error);
      }
      
    }
  },
 async mounted(){
    try {
        const songId = this.$store.state.route.params.songId
        this.song = (await SongsService.show(songId)).data
      } catch (error) {
        console.log(error);
        
      }
  }
}
</script>
<style>

</style>
