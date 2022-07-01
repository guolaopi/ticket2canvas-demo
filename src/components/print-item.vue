<template>
    <div class="print-item">
        <span class="setting-item">
            type:
            <select v-model="info.type">
                <option value="text">text</option>
                <option value="barcode">barcode</option>
                <option value="qrcode">qrcode</option>
                <option value="line">line</option>
            </select>
        </span>
        <span class="setting-item">
            content: <input type="text" v-model="info.content" />
        </span>
        <span class="setting-item">
            fontSize: <input type="text" v-model="info.fontSize" />
        </span>
        <span class="setting-item">
            fontFamily: <input type="text" v-model="info.fontFamily" />
        </span>
        <br />
        <span class="setting-item">
            bold: <input type="checkbox" v-model="info.bold" />
        </span>
        <span class="setting-item">
            width: <input type="text" v-model="info.width" />
        </span>
        <span class="setting-item">
            height: <input type="text" v-model="info.height" />
        </span>
        <span class="setting-item">
            left: <input type="text" v-model="info.left" />
        </span>
        <span class="setting-item">
            top: <input type="text" v-model="info.top" />
        </span>
    </div>
</template>

<script setup>
const props = defineProps({ info: Object });
</script>

<style>
.print-item {
    padding: 10px 0;
    border-top: 2px solid #aaa;
}
.print-item:nth-of-type(1) {
    border-top: 2px solid transparent;
}
</style>