<script setup>
  import { JsonForms } from '@jsonforms/vue'
  import { extendedVuetifyRenderers } from '@jsonforms/vue-vuetify'
  import { markRaw, ref } from 'vue'

  const renderers = markRaw([
    ...extendedVuetifyRenderers,
  // here you can add custom renderers
  ])
  // Reactive data properties
  const data = ref({
    name: '',
    email: '',
    age: 0,
  })

  const schema = ref({
    type: 'object',
    properties: {
      name: {
        type: 'string',
        title: 'Name',
      },
      email: {
        type: 'string',
        format: 'email',
        title: 'Email',
      },
      age: {
        type: 'integer',
        title: 'Age',
        minimum: 0,
      },
    },
    required: ['name', 'email'],
  })

  const uischema = ref({
    type: 'VerticalLayout',
    elements: [
      {
        type: 'Control',
        scope: '#/properties/name',
      },
      {
        type: 'Control',
        scope: '#/properties/email',
      },
      {
        type: 'Control',
        scope: '#/properties/age',
      },
    ],
  })
  // Methods
  const onChange = event => {
    data.value = event.data
  }
</script>

<template>
  <json-forms
    :data="data"
    :renderers="renderers"
    :schema="schema"
    :uischema="uischema"
    @change="onChange"
  />
</template>

<style>
@import '@jsonforms/vue-vuetify/lib/jsonforms-vue-vuetify.css';
</style>
