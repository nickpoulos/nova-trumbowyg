<template>
    <default-field :field="field" :full-width-content="true">
        <template slot="field">
            <div :class="[errorClasses, errorClasses.length ? 'border' : '']" @keydown.stop>
                <trumbowyg v-model="value" :config="field.options"></trumbowyg>
            </div>

            <p v-if="hasError" class="my-2 text-danger">
                {{ firstError }}
            </p>
        </template>
    </default-field>
</template>

<script>
    import { FormField, HandlesValidationErrors } from 'laravel-nova'
    import trumbowyg from 'vue-trumbowyg';
    import 'trumbowyg/dist/ui/trumbowyg.css';
    import 'trumbowyg/dist/plugins/upload/trumbowyg.upload';
    import 'trumbowyg/dist/plugins/emoji/trumbowyg.emoji';
    import 'trumbowyg/dist/plugins/table/trumbowyg.table';
    import 'jquery-resizable/resizable';
    import 'jquery-resizable/resizable.css';
    import 'trumbowyg/dist/plugins/resizimg/trumbowyg.resizimg';
    import 'trumbowyg/dist/plugins/cleanpaste/trumbowyg.cleanpaste';
    import 'trumbowyg/dist/plugins/pasteembed/trumbowyg.pasteembed';

export default {
    mixins: [FormField, HandlesValidationErrors],

    props: ['resourceName', 'resourceId', 'field'],

    methods: {
        /*
         * Set the initial, internal value for the field.
         */
        setInitialValue() {
          this.value = this.field.value || ''
        },

        /**
         * Fill the given FormData object with the field's internal value.
         */
        fill(formData) {
          formData.append(this.field.attribute, this.value || '')
        },

        /**
         * Update the field's internal value.
         */
        handleChange(value) {
          this.value = value
        }
    },

    components: {
        trumbowyg
    }
}
</script>
