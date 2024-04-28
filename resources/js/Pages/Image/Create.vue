<template>
    <Head title="Dashboard" />

    <!-- <BreezeAuthenticatedLayout> -->
        <!-- <template #header> -->
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Image Create
            </h2>
        <!-- </template> -->

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <form @submit.prevent="submit">
                            <div>
                                <label for="File">File Upload</label>
                                <input
                                    type="file"
                                    @change="previewImage"
                                    ref="photo"
                                    class="
                                        w-full
                                        px-4
                                        py-2
                                        mt-2
                                        border
                                        rounded-md
                                        focus:outline-none
                                        focus:ring-1
                                        focus:ring-blue-600
                                    "
                                />
                                <img
                                    v-if="url"
                                    :src="url"
                                    class="w-full mt-4 h-80"
                                />
                                <div
                                    v-if="errors.image"
                                    class="font-bold text-red-600"
                                >
                                    {{ errors.image }}
                                </div>
                            </div>

                            <div class="flex items-center mt-4">
                                <button
                                    class="
                                        px-6
                                        py-2
                                        text-white
                                        bg-gray-900
                                        rounded
                                    "
                                >
                                    Save
                                </button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    <!-- </BreezeAuthenticatedLayout> -->
</template>

<script>
// import BreezeAuthenticatedLayout from "../../AuthenticatedLayout.vue";
// import BreezeLabel from "@/Components/Label";
import { Head } from "@inertiajs/vue3";
import { useForm } from "@inertiajs/vue3";
export default {
    components: {
        // BreezeAuthenticatedLayout,
        Head,
    },
    props: {
        errors: Object,
    },
 data() {
    return {
      url: null,
    }
  },
    setup() {
        const form = useForm({
            image: null,
        });

        return { form };
    },
    methods: {
        submit() {
            if (this.$refs.photo) {
                this.form.image = this.$refs.photo.files[0];
            }
            this.form.post(route("image.store"));
        },
        previewImage(e) {
            const file = e.target.files[0];
            this.url = URL.createObjectURL(file);
        },
    },
};
</script>
