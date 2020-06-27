<template>
    <button class="g-button" :class="{ [`icon-${iconPosition}`]: true }">
        <svg v-if="icon" class="icon" aria-hidden="true">
            <use :xlink:href="`#i-${icon}`"></use>
        </svg>
        <div class="content">
            <slot></slot>
        </div>
    </button>
</template>
<script>
export default {
    // props: ['icon', 'iconPosition'],
    props: {
        icon: {},
        iconPosition: {
            type: String,
            default: 'left',
        },
        // 检查器，防止用户输入不合理的参数，比如'up'
        validator(value) {
            return value === 'left' || value === 'right'
        },
    },
}
</script>
<style lang="scss">
.g-button {
    height: var(--button-height);
    font-size: var(--font-size);
    padding: 0 1em;
    border-radius: var(--border-radius);
    border: 1px solid var(--border-color);
    background: var(--button-bg);
    display: inline-flex;
    vertical-align: middle; // 内联元素，不能使用默认值，否则对不齐
    justify-content: center;
    align-items: center;
    &:hover {
        border-color: var(--border-hover-color);
    }
    &:active {
        background-color: var(--button-active-bg);
    }
    &:focus {
        outline: none;
    }
    > .icon {
        order: 1;
        margin-right: 0.2em;
    }
    > .content {
        order: 2;
    }
    &.icon-right {
        > .icon {
            order: 2;
            margin-right: 0;
            margin-left: 0.2em;
        }

        > .content {
            order: 1;
        }
    }
}
</style>
