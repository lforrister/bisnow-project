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
    </div>
</template>

<script>
export default {
  name: 'Email Directory',
  methods: {
    emailSearch() {
      //Here is where we'll search through the directory
      console.log('searching!')
    }
  }
}
</script>

<style lang="scss">
</style>
