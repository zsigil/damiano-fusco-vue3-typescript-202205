<template>
    <li :class="cssClass" @click="onClick">
        <div class="selected-indicator">*</div>
        <div class="name">{{ model.name }}</div>
    </li>
</template>

<script lang="ts">  
import { defineComponent, computed, PropType } from 'vue'
import { ItemInterface } from '@/models/items/Item.interface'

export default defineComponent({
    props: {
        model: {
            type: Object as PropType<ItemInterface>
        }
    },
    emits: ['select'],
    setup(props, { emit }) {
        const cssClass = computed(() => {
        let css = 'item'
        if (props.model?.selected) {
            css += ' selected'
        }
        return css.trim()
        })

        const onClick = () => {
            emit('select', props.model) 
        }

        return {
            cssClass,
            onClick
        }
    }
})
</script>

<style lang="scss">
li.item {
    padding: 0;
    outline: solid 1px #eee;
    display: grid;
    grid-template-columns: 1.7em auto;
    cursor: pointer;
    transition: background-color 0.3s ease;
    .name {
        padding: 5px;
        text-align: left;
    }
    .selected-indicator {
        padding: 5px;
        font-size: 3em;
        line-height: 0.5em;
        padding: 5px;
        color: lightgray;
    }
    &.selected {
    .selected-indicator {
        color: skyblue;
    }
    }
    &:hover {
        background-color: #eee;
    }
}
</style>
