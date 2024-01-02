<script setup>
    import { defineProps, ref, computed, defineExpose } from 'vue';

    const props = defineProps({
        data: Object,
    })

    props.data.currentStep--;

    const data = ref(props.data);

    const cssStyle = computed( () => {
        return {
            '--active-color': data.value.activeColor,
            '--passive-color': data.value.passiveColor,

        };
    })

    const nextStep = () => {
        if(data.value.currentStep < data.value.steps.length -1){
            data.value.currentStep++;
            console.log(data.value.currentStep);
        }
    };

    const previousStep = () => {
        if(data.value.currentStep > 0){
            data.value.currentStep--;
        }
    };

    defineExpose({
        nextStep,
        previousStep,
    })


</script>

<template>

    <div class="steps-container" :style="cssStyle">
        <ul class="step-list">
            <li class="step" v-for="(step, index) in data.steps" :key="index" :class="(index == data.currentStep) ? 'step-active' : '', (index < data.currentStep) ? 'step-done' : '', (index == 0 && index == data.currentStep) ? 'step-done-in-advance' : ''">
                <div class="step-bubble">
                    <div class="step-count"> {{ index + 1 }} </div>
                </div>
                <div class="step-line"> 
                    <div class="line-fill"> </div>
                </div>
            </li>
        </ul>
    </div>

    Hello World!
</template>

<style scoped>
    .step-container {
        width: 95%;
        margin: 0 auto;
    }

    .step-list {
        display: flex;
        list-style: none;
    }

    .step {
        display: flex;
        align-items: center;
        flex-grow: 1;
        max-width: 100%;
        position: relative;
        height: 60px;
    }

    .step-bubble {
        width: 35px;
        height: 35px;
        border-radius: 50%;
        background-color: var(--passive-color);
        transition: all .3% ease;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .step-line {
        width: 100%;
        height: 5px;
        position: absolute;
        background-color: var(--passive-color);
        top: 50%;
        left: 0;
        transform: translateY(-50%);
        z-index: -10;
    }

    .step-fill {
        width: 0;
        height: 5px;
        background-color: (--active-color);
        transition: all .3s ease;
    }

    .step:last-child {
        max-width: 60px;
    }

    .step:last-child .step-line {
        display: none;
    }

    .step-active .step-bubble {
        width: 60px;
        height: 60px;
    }

    .step-active .step-count {
        display: block;
    }

    .step-done .step-bubble {
        width: 60px;
        height: 60px;
    }

    .step-done .line-fill {
        width: 100%;
    }

    .step-done-in-advance .line-fill{
        width: 50%;
    }

    .step-count {
        color: white;
        font-weight: 500;
        font-size: 20px;
        display: none;
    }

    

</style>