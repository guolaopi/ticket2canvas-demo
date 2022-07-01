<template>
    <div class="section">
        <h3>Canvas(Ticket) setting</h3>
        <span class="setting-item">
            canvas(ticket) width:
            <input type="text" v-model="cvsWidth" />
        </span>
        <span class="setting-item">
            canvas(ticket) height:
            <input type="text" v-model="cvsHeight" />
        </span>
    </div>
    <div class="section">
        <h3>
            Print items
            <button class="big-btn" @click="add">add item</button>
        </h3>
        <print-item v-for="item in items" :key="item.id" :info="item" />
    </div>
    <div class="section">
        <h3>
            Preview
            <button class="big-btn" @click="clickFunc">ticket2canvas</button>
            <button class="big-btn" @click="print">print</button>
        </h3>
        <span class="result-item">
            Canvas:
            <br />
            <canvas id="cvs"></canvas>
        </span>
        <span class="result-item">
            Image:
            <br />
            <img id="img" ref="imgRef" :src="imgSrc" alt="result img" />
        </span>
    </div>
</template>


<script setup>
import { reactive, ref } from "vue";
import ticket2canvas from "ticket2canvas";
import PrintItem from "./components/print-item.vue";

const imgSrc = ref("");
const imgRef = ref();
const cvsWidth = ref(200);
const cvsHeight = ref(400);
const items = reactive([
    {
        id: 1,
        type: "text",
        content: "Ticket Title",
        fontSize: 30,
        fontFamily: "Microsoft YaHei",
        bold: true,
        left: 20,
        top: 20,
        height: 30,
    },
    {
        id: 2,
        type: "text",
        content: "hello world",
        fontSize: 20,
        fontFamily: "Agency FB",
        bold: true,
        left: 20,
        top: 140,
        height: 20,
    },
    {
        id: 3,
        type: "barcode",
        content: "123456",
        width: 280,
        height: 30,
        left: 10,
        top: 80,
    },
    {
        id: 4,
        type: "line",
        width: 160,
        height: 3,
        left: 20,
        top: 180,
    },
    {
        id: 5,
        type: "text",
        content: "that is a line above",
        fontSize: 16,
        fontFamily: "PingFang",
        left: 70,
        top: 190,
    },
    {
        id: 6,
        type: "qrcode",
        content: "654321",
        width: 180,
        height: 180,
        left: 10,
        top: 220,
    },
]);

async function clickFunc() {
    const bs64 = await ticket2canvas({
        el: "#cvs",
        printData: {
            width: cvsWidth.value,
            height: cvsHeight.value,
            list: items,
        },
    });
    imgSrc.value = bs64;
}

function add() {
    items.push({
        id: items.length,
        type: "text",
        content: "hello world",
        fontSize: 16,
        fontFamily: "Microsoft YaHei",
        bold: true,
        width: 200,
        height: 200,
        left: 20,
        top: 20,
    });
}

function print() {
    const win = window.open("", "_blank");
    win.document.body.innerHTML = imgRef.value.outerHTML;
    win.print();
}
</script>

<style>
.section {
    padding: 10px;
    margin: 10px 0;
    border: 2px solid salmon;
    border-radius: 10px;
}
.setting-item {
    display: inline-block;
    margin: 5px 30px 5px 5px;
}
.big-btn {
    font-size: 18px;
    padding: 5px;
}
.result-item {
    display: inline-block;
    vertical-align: top;
    margin: 10px;
}
#cvs {
    border: 1px solid skyblue;
}
#img {
    border: 1px solid greenyellow;
}
</style>