<template>
  <div>

    <div v-if="signedIn">
      <div class="form-group">
          <textarea name="body" id="body" class="form-control" placeholder="Have something to say?" rows="5"
                    v-model="body" required></textarea>
      </div>
      <button type="submit" class="btn btn-default" @click="addReply">Post</button>
    </div>

    <p class="text-center" v-else>Please <a href="/login">sign in</a> to participate to this discussion!</p>

  </div>
</template>

<script>
  export default {
    name: 'NewReply',

    data() {
      return {
        body: ''
      }
    },

    computed: {
      signedIn() {
        return window.App.signedIn;
      }
    },

    methods: {
      addReply()
      {
        axios.post(location.pathname + '/replies', { body: this.body })
          .then(({ data }) => {
            this.body = '';
            flash('Your reply has been posted!');
            this.$emit('created', data);
          });
      }
    }
  }
  ;
</script>

<style>

</style>