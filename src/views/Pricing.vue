<template>
    <div class="flex justify-center">
        <div class="w-1/2 bg-blue-900 rounded-lg shadow px-6 py-12 flex flex-col items-center">
            <div class="bg-gray-400 rounded-full flex justify-around p-1">
                <button @click="currentFrequency = frequency "
                    v-for="(price, frequency) in plans[0].pricing"
                    :key="(price.id, frequency.id)"
                    class="rounded-full text-xs font-bold px-6 py-1 uppercase focus:outline-none "
                    :class="currentFrequency == frequency ? 'bg-blue-600 text-gray-200' : '' "
                >{{ frequency }}</button>
                
            </div>

            <div class="flex w-full pt-8">
                <div v-for="plan in plans" :key="plan.id" class="text-white w-1/2">
                    <h1 class="text-2xl font-bold">{{plan.name}}</h1>

                    <ul class="pt-4">
                        <li v-for="benefit in plan.benefits[currentFrequency]" :key="benefit">{{benefit}}</li>
                    </ul>

                    <div class="flex justify-center pt-8">
                        <div class="text-4xl font-bold">${{ plan.pricing[currentFrequency].price }}</div>
                        <div class="pl-1 pt-2 text-gray-300">{{ plan.pricing[currentFrequency].label }}</div>
                    </div>
                </div>

                
            </div>

            <div class="pt-4 text-center text-gray-400 text-sm font-bold">
                
            </div>

        </div>
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            currentFrequency: 'monthly',
            plans: [
                {
                    name: "Starter",
                    benefits: {
                        monthly: ['benefits1','benefits2','benefits3'],
                        yearly: ['benefits1','benefits2','benefits3','benefits4'],
                        lifetime: ['benefits1','benefits2','benefits3','benefits4', 'benefits5'],
                    },

                    pricing: {
                        monthly: { price: 99, label: '/mo'},
                        yearly: { price: 199, label: '/yr'},
                        lifetime: { price: 399, label: ''}
                    }
                },
                {
                    name: "Pro",
                    benefits: {
                        monthly: ['benefits1','benefits2','benefits3'],
                        yearly: ['benefits1','benefits2','benefits3','benefits4'],
                        lifetime: ['benefits1','benefits2','benefits3','benefits4', 'benefits5'],
                    },

                    pricing: {
                        monthly: {price: 399, label: '/mo'},
                        yearly: {price: 1099, label: '/yr'},
                        lifetime: { price: 1399, label: ''}
                    }
                }
            ]
        }
    }
}
</script>