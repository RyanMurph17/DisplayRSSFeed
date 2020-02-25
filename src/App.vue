
  <template>
    <div id="app">
      <ul>
        <feed v-for="feed in feeds" :feed="feed" :key="feed.title"></feed>
       </ul>
    </div>
  </template>


<script>
import io from 'socket.io-client'
   import Feed from './components/Feed.vue'
   export default {
      components: {
         Feed
      },
      data () {
         return {
            feeds: []
         }
      },
      mounted() {
         this.subscribeToFeed();
      },
      methods: {
         subscribeToFeed() {
            const socket = io('http://localhost:8081');
            socket.on('feed', data => {
               this.feeds = [...data.feed]
            });
         }
      }
   }
</script>
