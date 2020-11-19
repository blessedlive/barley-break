<template>
    <div class="cell" :class="{'hide': index < 1}">
        {{ index }}
    </div>
</template>

<script>
export default {
    props: {
        index: Number
    }
}
</script>