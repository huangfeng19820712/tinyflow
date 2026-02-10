<template>
    <div style="width: 100%; height: calc(100vh - 16px)">
        <div style="margin-bottom:8px; display:flex; gap:8px">
            <button @click="handleGetData">获取数据</button>
            <button @click="handleSetData">设置数据</button>
        </div>
        <Tinyflow
            className="custom-class"
            :style="{ width: '100%', height: '100%' }"
            :data="initialData"
            :provider="provider"
            ref="tinyflowRef"
        />

    </div>
</template>

<script setup lang="ts">
import { Tinyflow } from '@tinyflow-ai/vue';
import '@tinyflow-ai/vue/dist/index.css';
import { ref } from 'vue';

const tinyflowRef = ref<InstanceType<typeof Tinyflow> | null>(null);


const provider = {
    llm: ()  => [
        {
            value: 'llm',
            label: 'llm',
        }
    ],
    knowledge: () => [],
}
const initialData = ref({
    nodes: [],
    edges: [],
    viewport: {
        x: -1000,
        y: -1000,
        zoom: 1,
    },
});

const handleGetData = () => {
    if (tinyflowRef.value) {
        const data = tinyflowRef.value.getData();
        console.log('Tinyflow data:', data);
    } else {
        console.warn('Tinyflow component ref is not ready');
    }
};
const handleSetData = () => {
    if (tinyflowRef.value) {
        let data = tinyflowRef.value.getData();
        if(data){
            data.viewport = {
                x: 500,
                y: 400,
                zoom: 1,
            }
            tinyflowRef.value.getInstance()?.setData(data);
        }
        console.log('Tinyflow data:', data);
    } else {
        console.warn('Tinyflow component ref is not ready');
    }
};
</script>
