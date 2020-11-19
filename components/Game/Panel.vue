<template>
    <div class="counter">
        <span class="name">{{ name }}</span>
        <span class="value">{{ value }}</span>
    </div>
</template>

<script>
export default {
    props: {
        name: String,
        value: [String, Number]
    }
}
</script>