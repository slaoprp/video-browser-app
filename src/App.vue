<template>
  <div>
    <SearchBar v-on:termChange="onTermChange" />
    <VideoList 
      v-for="video in videos"
      :key="video.id" 
      :id="video.id"
    />
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar'
import VideoList from './components/videoList/VideoList'
const API_KEY = 'AIzaSyBcgl2qhPf5DMfPwwrhMUR9jqqxwh5CxXo';

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList
  },
  data() {
    return {
      videos: []
    }
  },
  methods: {
    onTermChange(searchTerm) {
      axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
          key: API_KEY,
          type: 'video',
          part: 'snippet',
          q: searchTerm
        }
      }).then(response => {
        this.videos = response.data.items
      })
      console.log(this.videos)
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
