<template>
    <v-container>
      <v-row>
          <v-col md="3" cols="12">
              <h1>Video Create Page</h1>
              <VideoEditForm :video="video" :saveVideo="createVideo" buttonText="Create Video"/>
          </v-col>
          <v-col md="9" cols="12">
              <VideoListVideo :video="video" />
          </v-col>
      </v-row>
    </v-container>
    
</template>

<script>
import VideoListVideo from '@/components/VideoListVideo';
import VideoEditForm from '@/components/VideoEditForm.vue';

export default {
    data() {
      return {
        video: {},

        required(propertyType) { 
          return v => v && v.length > 0 || `You must input a ${propertyType}`
        },
        minLength(propertyType, minLength) {
          return v => v && v.length >= minLength || `${propertyType} must be at least ${minLength} characters`
        },
        maxLength(propertyType, maxLength) {
          return v => v && v.length <= maxLength || `${propertyType} must be less than ${maxLength} characters`
        }
    
      }
    },
    components: {
      VideoListVideo,
      VideoEditForm
    },
    methods: {
      async createVideo() {
        let video = await this.$store.dispatch('videos/createVideo', this.video);
        this.$store.dispatch('snackbar/setSnackbar', {
          text: `You have successfully created a new video, ${video.name}`
        });
        this.$router.push({ name: 'video-watch', params: {id: video.id}});
      }
    },
    
}
</script>

<style lang=scss scoped>

</style>