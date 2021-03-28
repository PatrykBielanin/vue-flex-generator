<template>
    <div :style="{height: height+'px', width: width+'px', margin: margin+'px', backgroundColor: backgroundColor}" >
    </div>
</template>

<script>
    export default {
        name: "FlexItem",
        props: ['height', 'width', 'margin', 'backgroundColor']
    }
</script>
