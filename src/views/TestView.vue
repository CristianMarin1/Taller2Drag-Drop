<template>
    <div>
        <h1>Hola desde TestView</h1>
        <TestComponent msg="hola mundo"/>
    </div>
</template>

<script>
// @ is an alias to /src
import TestComponent from '@/components/TestComponent.vue'

export default {
    name: "TestView",
    components: {
        TestComponent
    }
}
</script>
