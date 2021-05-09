<template>
    <breeze-authenticated-layout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Edit
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-2xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="w-full py-3 px-4 border-b ">
                        <h2 class="font-semibold text-md text-gray-800 leading-tight">
                            Edit employee information
                        </h2>
                    </div>
                    <form @submit.prevent="submit" class="w-full py-4 px-4 flex flex-col space-y-4 text-gray-700">
                            <breeze-validation-errors class="mb-4" />
                            <div class="flex justify-between space-x-2">
                                <div class="w-full flex flex-col space-y-1">
                                    <label for="name">Name:</label>
                                    <input v-model="form.name" type="text" placeholder="Name" class="w-full rounded" required>
                                </div>
                                <div class="w-full flex flex-col space-y-1">
                                    <label for="name">Email:</label>
                                    <input v-model="form.email" type="email" placeholder="Email" class="w-full rounded" required>
                                </div>
                            </div>
                           <div class="flex flex-col space-y-1">
                               <label for="name">Address:</label>
                               <input v-model="form.address" type="text" placeholder="Address" class="rounded" required>
                           </div>
                           <div class="w-full">
                                <button type="submit" class="w-full mt-4 py-2 bg-gradient-to-r from-green-400 to-blue-500 text-white font-semibold rounded hover:bg-gradient-to-l hover:from-blue-400 hover:to-green-500">
                                    Save
                                </button>
                           </div>
                       </form>
                </div>
            </div>
        </div>
    </breeze-authenticated-layout>
</template>

<script>
    import BreezeAuthenticatedLayout from '@/Layouts/Authenticated'
    import BreezeValidationErrors from '@/Components/ValidationErrors'

    export default {
        components: {
            BreezeAuthenticatedLayout,
            BreezeValidationErrors

        },

        props: {
            auth: Object,
            errors: Object,
            employee: Object,
        },

        data() {
            return {
                form: this.$inertia.form({
                    name: this.employee.name,
                    email: this.employee.email,
                    address: this.employee.email
                })
            }
        },

        methods: {
            submit() {
                this.form
                    .transform(data => ({
                        ... data,
                        remember: this.form.remember ? 'on' : ''
                    }))
                    .put(this.route('employees.update', this.employee), {
                       //code
                    })
            },

            hasErrors() {
                return false;
            },
        }
    }
</script>
