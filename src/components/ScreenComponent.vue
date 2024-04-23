<template lang="pug">
.screen(ref="screen") {{ result }}
</template>

<script>
export default {
    props: ["result"]
}
</script>

<style lang="scss">
.screen {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    padding: 10px;
    background-color: var(--screenBg);
    color: var(--textColor2);
    font-size: 38px;
    height: 90px;
    border-radius: var(--radius);
    margin-bottom: 20px;
    white-space: nowrap;
    overflow: hidden;
    transition: var(--transition2);
}
</style>