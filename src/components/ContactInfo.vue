<template>
    <div>
        <h2>{{ selectedContact.name }}</h2>
        <div>
            <p>{{ selectedContact.email }}</p>
            <div v-for="phone in selectedContact.phone" :key="phone.number">
                {{ formattedPhone(phone) }}
            </div>
            <p> {{ selectedContact.city }}, {{ selectedContact.state }}, {{ selectedContact.postal_code}}, {{ selectedContact.country }} </p>
        </div>
    </div>
</template>

<script>
export default ({
    name: 'Contact Info',
    props: {
        selectedContact: {
            type: Object,
            default: null,
        }
    },
    methods: {
        formattedPhone(phone) {
            return `+${phone.country_code} (${phone.area_code})-${phone.number}`
        }
    }
})
</script>
