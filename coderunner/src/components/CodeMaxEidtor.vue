<script setup lang="ts">
import { ref } from 'vue'

import { RunCodeRequest } from "./runcode";

import CodeEditor from "./SimpleCodeEditor.vue"

const CodeData = ref("");

const OutputResult = ref("");


const RunCodeAction = async () => {
    const payload = {
        "language": "python3",
        "code": CodeData.value,
        "timestamp": Date.now()
    }
    const resp = await RunCodeRequest(payload);

    OutputResult.value = resp.result;
}

const Languages = ref([['python', 'Python'], ['rust', "Rust"], ['go', "Go"], ['javascript', 'JS']]);
</script>

<template>
    <div style="width: 980px;margin: 0 auto;margin-top: 60px;">
        <CodeEditor :autofocus="true" min_height="140px" v-model="CodeData" :language_selector="true" min_width="980px" :languages="Languages" />
        <div style="margin-top: 24px;width: 60px">
            <button @click="RunCodeAction" style="color: #fff">Run</button>
        </div>
        <div  v-if="OutputResult" class="OutputBox">
            <pre>{{ OutputResult }}</pre>
        </div>
    </div>
</template>

<style scoped>
.OutputBox {
    margin-top: 24px; 
    padding: 12px 20px 12px 20px; 
    width:940px;
    color: #abb2bf;
    border-radius: 12px;
    background: #282c34;
    font-family: Monaco, monospace;
    line-height: 1.5;
    font-size: 16px;
    overflow: auto;
    max-height: 300px;

}
.OutputBox pre {
    font-family: Monaco, monospace;
    font-size: 16px;
    font-weight: bold;
    line-height: 1.5;
    color: #fbfcfa;
}
</style>
