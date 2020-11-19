<template>
    <div class="keyboard">
        <div class="key" @click="onPress(1)">←</div>
        <div class="separator">   
            <div class="key" @click="onPress(4)">↑</div>
            <div class="key" @click="onPress(-4)">↓</div>
        </div>
        <div class="key" @click="onPress(-1)">→</div>
    </div>
</template>

<script>
export default {
    props: {
        onPress: Function
    }
}
</script>