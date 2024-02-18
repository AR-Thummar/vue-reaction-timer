<template>
    <p>Reaction time - {{ score }} ms</p>
    <p class="rank">{{ rank }} - {{ isEligible ? "You are Eligible for Signup" : "Please try again" }}</p>
    <SignupForm v-if="isEligible" />
</template>
  
<script>
import SignupForm from './SignupForm.vue'
export default {
    props: ['score'],
    components: {
        SignupForm
    },
    data() {
        return {
            rank: null,
            isEligible: false
        }
    },
    mounted() {
        if (this.score < 300) {
            this.rank = '1st'
            this.isEligible = true
        } else if (this.score < 550) {
            this.rank = '2nd'
            this.isEligible = true
        } else {
            this.rank = '3rd'
        }
    }
}
</script>
  
<style>
.rank {
    font-size: 1.4em;
    color: #0faf87;
    font-weight: bold;
}
</style>