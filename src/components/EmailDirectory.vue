<template>
    <div class="bg-white max-w-lg mx-auto p-8 bg-white md:shadow-md rounded-md">
        <div class="border-b-2 border-color-gray-900 pb-3">
            <h1 class="text-lg font-bold leading-6 text-gray-900 text-center">
                Email Directory 
            </h1>
            <p class="text-sm font-light text-gray-900 italic pt-2">
                Please enter an email in the field below to retrieve the associated information.
            </p>
        </div>

        <form class="pt-4">
            <div v-if="errorMessage" class="border-2 border-red-600 rounded-sm p-2 text-xs text-red-600 bg-red-50 font-bold mb-4">
                {{ errorMessage }}
            </div>
            <div class="mb-4">
                <label class="block text-gray-500 text-xs font-bold mb-2 uppercase" for="email">
                    Email Address
                </label>
                <input
                    v-model="emailInput"
                    class="emailDirectory__input shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    :class="{'is-invalid' : invalidMessage, 'has-error' : errorMessage}"
                    id="email"
                    type="email"
                    placeholder="Email"
                    required
                    @input="validateEmail"
                    @blur="checkToSubmit"
                    @keydown="clearMessaging"
                />
                <div v-if="invalidMessage" class="text-xs italic text-red-600 pt-2">
                    {{ invalidMessage }}
                </div>
            </div>

            <button
                :disabled="disabled"
                type="submit"
                :class="{'is-disabled' : disabled}"
                class="emailDirectory__button w-full bg-blue-400 text-white font-bold py-2 px-4 rounded hover:bg-blue-900"
                @click.prevent="emailSearch()"
            >
                Submit
            </button>
        </form>

        <ContactInfo v-if="includedEmail" :selectedContact="selectedContact" />
    </div>
</template>

<script>
import contacts from '../assets/json/contacts.json'
import ContactInfo from './ContactInfo.vue'

export default {
  name: 'EmailDirectory',
  components: {
      ContactInfo,
  },
  data() {
      return {
          contactData: contacts,
          emailInput: null,
          includedEmail: false,
          selectedContact: {},
          errorMessage: null,
          invalidMessage: null,
          timeout: null,
          disabled: true,
      }
  },
  watch: {
      emailInput() {
          if (!this.emailInput.length) {
              this.disabled = true
          }
      }
  },
  methods: {
    validateEmail() {
        //This will run on input with a timeout of 1 second - this is so it can trigger while they're still in the input field, but theoretically when they have paused typing
        clearTimeout(this.timeout)

        const emailRegex = /\b[\w.!#$%&’*+/=?^`{|}~-]+@[\w-]+(?:\.[\w-]+)*\b/
        const valid = emailRegex.test(this.emailInput)

        /*I think the best experience is to trigger if it's valid, but not if it's empty. 
        If it's empty, they may be thinking or not ready to fully interact yet, and the error feels distracting.
         We'll catch the empty on blur, so it will still fire a message when they leave the input field. */
        if (!valid && this.emailInput.length) {
            this.timeout = setTimeout(() => {
                this.invalidMessage = 'Please enter a valid email address'
                this.disabled = true
            }, 1000)
        } else {
            this.invalidMessage = null
            this.disabled = false
        }
    },
    checkToSubmit() {
        //This will run on blur/when they exit the input field in some way
        const emailRegex = /\b[\w.!#$%&’*+/=?^`{|}~-]+@[\w-]+(?:\.[\w-]+)*\b/
        const valid = emailRegex.test(this.emailInput)

        if (!valid) {
            this.invalidMessage = 'Please enter a valid email address'
            this.disabled = true
        } else {
            this.invalidMessage = null
            this.disabled = false
        }
    },
    emailSearch() {
      //Here is where we'll search through the directory
      const emails = this.contactData.map((contact) => contact.email)

      if (emails.includes(this.emailInput)) {
          this.includedEmail = true
          this.selectedContact = this.contactData.find((contact) => contact.email === this.emailInput)
          this.errorMessage = null
      } else {
          this.includedEmail = false
          this.selectedContact = {}
          this.errorMessage = "We're sorry, we couldn't find information associated with that email address. Please try again." 
      }

    },
    clearMessaging() {
        // Let's clear the not found message once they start a new input, so it doesn't linger
        if (this.errorMessage) {
            this.errorMessage = null
        }
    }
  }
}
</script>

<style lang="scss">
.emailDirectory__input {
    &.is-invalid,
    &.has-error {
        border: 2px solid #f87171;
    }
}

.emailDirectory__button {
    cursor: pointer;

    &.is-disabled {
        background: lightgray;
        cursor: not-allowed;

        &:hover {
            background: lightgray;
        }

        &:focus {
            outline: none;
        }
    }
}
</style>
