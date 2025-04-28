<script setup>
const props = defineProps({
  count: {
    type: Number,
    requred: true, // typo: should be 'required'
  },
  foo: {
    type: String,
    required: true,
  },
  label: {
    default: 123, // missing type, should be String
  },
  active: {
    type: Boolean,
    default: null, // Nullable boolean
  },
  items: {
    type: Array,
    default: () => undefined, // Undefined is not a valid default for an array
  },
  callback: {
    type: Function, // No default, but used as if always defined
  },
})

// Intentionally misspelled variable for demonstration
const doubled = props.cout * 2 // No error at build time!

// Invalid operation: trying to multiply a string by a number
// will result in "NaN" at runtime, but no error at build time
const bar = props.foo * 2 // No error at build time!

// Using label as a string, but default is a number
const labelUpper = props.label.toUpperCase()

// Items is undefined, but used as an array
const firstItem = props.items[0]

// Subtle: using callback as a function, but it may be undefined
const cbResult = props.callback()

// Subtle: using a property that doesn't exist
const notAProp = props.missingProp
</script>

<template>
  <div>
    <p>Count: {{ props.count }}</p>
    <p>Doubled: {{ doubled }}</p>
    <p>Bar: {{ bar }}</p>
    <p>Label Upper: {{ labelUpper }}</p>
    <p>First Item: {{ firstItem }}</p>
    <p>Callback Result: {{ cbResult }}</p>
    <p>Not a Prop: {{ notAProp }}</p>
  </div>
</template>
