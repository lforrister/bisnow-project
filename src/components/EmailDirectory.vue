<template>
    <div class="bg-white max-w-lg mx-auto p-8 bg-white md:shadow-md rounded-md">
        <h1> Email Directory </h1>
        <p>
            Please enter an email in the field below to retrieve the associated information.
        </p>

        <form>
            <div>
                <label>
                    Email Address
                </label>
                <input
                    v-model="emailInput"
                    id="email"
                    type="email"
                    placeholder="Email"
                    required
                />
            </div>

            <button
                type="submit"
                @click.prevent="emailSearch()"
            >
                Submit
            </button>
        </form>

        <div v-if="includedEmail">
            <h1> Contact Info: </h1>
            {{ selectedContact.name }}
        </div>

        <div v-if="errorMessage">
            {{ errorMessage }}
        </div>
    </div>
</template>

<script>
import contacts from '../assets/json/contacts.json'

export default {
  name: 'Email Directory',
  data() {
      return {
          contactData: contacts,
          emailInput: null,
          includedEmail: false,
          selectedContact: {},
          errorMessage: null,
      }
  },
  methods: {
    emailSearch() {
      //Here is where we'll search through the directory
      console.log('searching!')
      console.log('contacts', this.contacts)

      const emails = this.contactData.map((contact) => contact.email)

      console.log('emails', emails)

      if (emails.includes(this.emailInput)) {
          this.includedEmail = true
          this.selectedContact = this.contactData.find((contact) => contact.email === this.emailInput)
          this.errorMessage = null
      } else {
          this.includedEmail = false
          this.selectedContact = {}
          this.errorMessage = "We're sorry, we couldn't find information associated with that email address. Please try again." 
      }

    }
  }
}
</script>

<style lang="scss">
</style>
