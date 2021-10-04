<template>
    <div class="bg-gray-50 mt-5 mb-2 p-6 rounded-md">
        <h2 class="text-xl font-bold leading-6 text-gray-800 text-center uppercase">
            {{ selectedContact.name }}
        </h2>
        <div class="text-sm mt-1">
            <div class="flex flex-wrap justify-center">
                <p class="contactInfo__contact">
                    {{ selectedContact.email }}
                </p>
                <div v-for="phone in selectedContact.phone" :key="phone.number">
                    {{ formattedPhone(phone) }}
                </div>
            </div>
            <p class="text-center"> {{ selectedContact.city }}, {{ selectedContact.state }}, {{ selectedContact.postal_code}}, {{ selectedContact.country }} </p>
        </div>

        <div class="pt-4 mt-4 border-t-2 border-color-gray-900">
            <div v-for="(position, index) in selectedContact.employments" :key="`${position.title}-${index}`" class="text-center">
                <h3 v-if="position.primary" class="font-bold text-md">
                    Primary Employment 
                </h3>
                <h3 v-else class="font-bold text-md mt-4">
                    Additional Employment 
                </h3>
                <h4>
                    {{ position.title }} at {{ position.company }}
                </h4>
                <div class="flex flex-wrap justify-center">
                    <div class="flex text-sm">
                        <p class="font-bold mr-1">Classification:</p>
                        <p>{{ position.classification }}</p>
                        <span class="mx-2"> | </span>
                    </div>
                    <div class="flex text-sm">
                        <p class="font-bold mr-1">Industry:</p>
                        <p>{{ position.industry }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default ({
    name: 'ContactInfo',
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

<style lang="scss">
.contactInfo__contact {

    @media screen and (min-width: 768px) {
        position: relative;
        margin-right: 30px;

        &:after {
            content: '';
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            right: -18px;
            width: 4px;
            height: 4px;
            background: #6B7280;
            border-radius: 50%;
        }
    }
}

</style>