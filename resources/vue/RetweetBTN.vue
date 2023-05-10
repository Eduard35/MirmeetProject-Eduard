<template>
  <button v-if="btnRetweet" @click.prevent="makeRetweet()"
    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
    <i class="fas fa-retweet"></i> Retweet
  </button>

  <button v-if="!btnRetweet" @click.prevent="makeRetweet()">
    <i class="fas fa-retweet"></i> Retweeted
  </button>
</template>

<script>
import axios from 'axios';

export default {
  name: "Test",
  created() {},
  data() {
    return {
      btnRetweet: false,
      retweets: '',
      id_user: this.id_user,
      id_post: this.id_post
    };
  },
  props: {
    id_user: null,
    id_post: null
  },
  methods: {
    makeRetweet() {
      axios.get('make-retweet/' + this.id_user + '/' + this.id_post).then(res => {
        this.retweets = res.data;
        if (this.retweets == "OK") {
          this.btnRetweet = true;
        } else {
          this.btnRetweet = false;
        }
      });
    }

  },
};
</script>
