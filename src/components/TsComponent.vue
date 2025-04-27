<script setup lang="ts">
import { add, greet } from '@/helpers/js-helpers.js'
import { multiply, greetPerson } from '@/helpers/ts-helpers.js'
import { multiplyByTwo } from '@/helpers/js-importing-ts.js'
import { add2 } from '@/helpers/ts-importing-js'

interface Props {
  label: string
  count?: number
}

const props = defineProps<Props>()

const sum = add(props.count ?? 0, 7)
const product = multiply(props.count ?? 0, 7)
const greeting = greet(props.label)
const greetingPerson = greetPerson(props.label)
const multipliedByTwo = multiplyByTwo(props.count ?? 0)
const add2Result = add2(props.count ?? 0)
</script>

<template>
  <div>
    <h2>TS Component</h2>
    <p>{{ props.label }}: add({{ props.count ?? 0 }}, 7): {{ sum }}</p>
    <p>multiply({{ props.count ?? 0 }}, 7): {{ product }}</p>
    <p>{{ greeting }}</p>
    <p>{{ greetingPerson }}</p>
    <p>{{ multipliedByTwo }}</p>
    <p>{{ add2Result }}</p>
  </div>
</template>
