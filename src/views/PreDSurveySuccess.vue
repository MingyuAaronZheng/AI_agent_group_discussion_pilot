<template>
  <div class="container">
    <h1>Thank You for Participating!</h1>
    <p>Your responses have been successfully recorded.</p>
    <p>We appreciate your time and valuable input. Compensation will be sent to you shortly.</p>
    <p>Click the button below to go back to the prolific.</p>
    <b-button
      variant="primary"
      @click="goBack"
    >
      Go Back
    </b-button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'PreDSurveySuccess',
  methods: {
    goBack: function (event) {
      let body = new FormData()
      body.append('subject_id', this.$store.state.subject_id)
      body.append('status', 'success')
      axios.post(this.$root.server_url + 'submit_to_prolific', body)
        .then(response => {
          if (response.data.success === true) {
            window.location.href = response.data.prolific_url
          } else {
            alert('Some error happened!! Please leave comments and submit the HIT on Prolific.')
          }
        })
        .catch(e => {
          alert('Some error happened!! Please leave comments and submit the HIT on Prolific.')
        })
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
}

h1 {
  margin-bottom: 1rem;
}

p {
  margin: 0.5rem 0;
}
</style>
