<template>
    <div class="btnContainer" :style="containerStyle">
        <button :class="[btn_type, `hover-${props.hoverType}`]" :style="buttonStyle" @mouseenter="handleMouseEnter"
            @mouseleave="handleMouseLeave">
            {{ btnTitle }}
        </button>
    </div>
</template>

<script setup>
import { computed, ref } from 'vue';

const props = defineProps({
    btnType: {
        type: String,
        required: true
    },
    btnTitle: {
        type: String,
        default: "button"
    },
    hoverType: {
        type: String,
        default: "up"
    },
    width: {
        type: String,
        default: 'max-content'
    },
    height: {
        type: String,
        default: '80px'
    },
    fontSize: {
        type: String,
        default: '1rem'
    },
    fontWeight: {
        type: String,
        default: "700"
    },
    backgroundColor: {
        type: String,
        default: ''
    },
    color: {
        type: String,
        default: ''
    },
    transitionTime: {
        type: Number,
        default: 0.4
    },
    borderRadius:{
        type: String,
    }
});

const isHovered = ref(false);

const btn_type = computed(() => {
    switch (props.btnType) {
        case 'btn-rectangle':
            return 'rectBtn button-rectangle';
        case 'btn-rounded':
            return 'rectBtn button-rounded';
        case 'btn-circle':
            return 'button-circle';
        case 'btn-icon':
            return 'button-icon';
        case 'btn-shadow':
            return 'rectBtn button-shadow';
        case 'btn-outline':
            return 'rectBtn button-outline';
        case 'btn-glass':
            return 'rectBtn button-glass';
        case 'btn-gradient':
            return 'rectBtn button-gradient';
        case 'btn-text':
            return 'rectBtn button-text';
        case 'btn-ghost':
            return 'rectBtn button-ghost';
        default:
            return '';
    }
});

const containerStyle = computed(() => ({
    width: props.width,
    height: props.height,
}));

const buttonStyle = computed(() => {
    const defaultColors = getDefaultColors();
    let style = {
        fontSize: props.fontSize,
        fontWeight: props.fontWeight,
        transition: `all ${props.transitionTime}s ease`,
        position: 'relative',
        overflow: 'hidden',
    };

    switch (props.btnType) {
        case 'btn-gradient':
            style.background = props.backgroundColor || defaultColors.background;
            // style.color = "transparent";
            break;
        default:
            style.background = props.backgroundColor || defaultColors.background;
            style.color = props.color || defaultColors.color;
    }

    style = addBtnHoverColor(style);
    style = addBorderRadius(style);

    return style;
});

const getDefaultColors = () => {
    switch (props.btnType) {
        case 'btn-rectangle':
            return { background: '#008CBA', color: 'white' };
        case 'btn-rounded':
            return { background: '#4CAF50', color: 'white' };
        case 'btn-shadow':
            return { background: 'white', color: 'black' };
        case 'btn-glass':
            return { background: '#0000ffaa', color: 'white' };
        case 'btn-circle':
            return { background: '#f44336', color: 'white' };
        case 'btn-icon':
            return { background: 'yellow', color: 'black' };
        case 'btn-outline':
            return { background: 'transparent', color: '#008CBA', border: '2px solid #008CBA' };
        case 'btn-gradient':
            return { background: 'linear-gradient(45deg, #f44336, #4CAF50)', color: 'black' };
        case 'btn-text':
            return { background: 'transparent', color: '#4CAF50', border: '2px solid transparent' };
        case 'btn-ghost':
            return { background: 'transparent', color: 'white', border: '2px solid yellow' };
        default:
            return { background: '#008CBA', color: 'white' };
    }
};

const addBtnHoverColor = (style) => {
    if (isHovered.value) {
        switch (props.btnType) {
            case 'btn-outline':
            case 'btn-text':
            case 'btn-ghost':
                style.background = style.color;
                style.color = 'black';
                break;
            default:
                // Swap colors for non-transparent backgrounds
                [style.background, style.color] = [style.color, style.background];
        }
    }

    return style;
}

const addBorderRadius = (style) => {
    switch (props.btnType) {
        case 'btn-rounded':
        case 'btn-shadow':
        case 'btn-outline':
        case 'btn-glass':
        case 'btn-gradient':
        case 'btn-text':
        case 'btn-ghost':
            style.borderRadius = props.borderRadius || "5px";
            break;
        case 'btn-circle':
        case 'btn-icon':
            style.borderRadius = props.borderRadius || "50%";
            break;
        default:
            style.borderRadius = props.borderRadius || "0";
    }

    return style;
}

const handleMouseEnter = () => {
    isHovered.value = true;
};

const handleMouseLeave = () => {
    isHovered.value = false;
};

</script>


<style lang="scss" scoped>
.btnContainer {
    text-align: center;

    >* {
        width: 100%;
        height: 100%;
        transition: all 0.3s ease; // 부드러운 전환 효과 추가
    }

    .rectBtn {
        padding: 10px 20px;
    }

    /* 1. 기본 사각형 버튼 */
    .button-rectangle {
        border-radius: 0;
    }

    /* 2. 둥근 모서리 버튼 */
    .button-rounded {
        border-radius: 5px;
    }

    /* 3. 원형 버튼 */
    .button-circle {
        border-radius: 50%;
        line-height: 50px;
        height: 120%;
        width: auto;
        aspect-ratio: 1/1;
    }

    /* 4. 아이콘 버튼 */
    .button-icon {
        padding: 10px;
        border-radius: 50%;
    }

    /* 5. 그림자 버튼 */
    .button-shadow {
        border-radius: 5px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    /* 6. 테두리 버튼 */
    .button-outline {
        border: 2px solid #008CBA;
        border-radius: 5px;
    }

    /* 7. 유리 효과 버튼 */
    .button-glass {
        border-radius: 5px;
        backdrop-filter: blur(1.5rem);
    }

    /* 8. 그라디언트 버튼 */
    .button-gradient {
        border-radius: 5px;
    }

    /* 9. 텍스트 버튼 */
    .button-text {
        border-radius: 5px;
        text-decoration: underline;
    }

    /* 10. 고스트 버튼 */
    .button-ghost {
        border: 2px solid white;
        border-radius: 5px;
    }

    button {
        position: relative;
        overflow: hidden;
        z-index: 1;

        &::before {
            content: '';
            position: absolute;
            background-color: v-bind('props.color || getDefaultColors().color');
            z-index: -1;
            transition: all v-bind('props.transitionTime + "s"') ease;
        }

        &.hover-fill_out,
        // &.hover-fill_in,
        &.hover-fillV_in,
        &.hover-fillV_out,
        &.hover-fillH_in,
        &.hover-fillH_out {
            &::after {
                content: '';
                position: absolute;
                background-color: v-bind('props.color || getDefaultColors().color');
                z-index: -1;
                transition: all v-bind('props.transitionTime + "s"') ease;
            }
        }

        // &.hover-fillV_in::before {
        //     top: 100%;
        // }

        // &.hover-fillV_in::after {
        //     bottom: -100%;
        // }

        &.button-circle,
        &.button-icon {
            &::before {
                border-radius: 50%;
            }
        }

        &.hover-up::before,
        &.hover-down::before,
        &.hover-left::before,
        &.hover-right::before {
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
        }

        &.hover-up::before {
            transform: translateY(100%);
        }

        &.hover-down::before {
            transform: translateY(-100%);
        }

        &.hover-left::before {
            transform: translateX(100%);
        }

        &.hover-right::before {
            transform: translateX(-100%);
        }

        &.hover-fill_out::before {
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            border-radius: 50%;
            transform: translate(-50%, -50%) scale(1);
        }

        &.hover-fill_in::before {
            top: 50%;
            left: 50%;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            transform: translate(-50%, -50%) scale(1);
            background-color: black;
            opacity: 0;
            transition: opacity v-bind('props.transitionTime/4 + "s"'), transform v-bind('props.transitionTime + "s"');
        }

        &.hover-fillV_in::before,
        &.hover-fillV_in::after {
            left: 0;
            right: 0;
            height: 0;
        }

        &.hover-fillV_in::before {
            top: 0;
        }

        &.hover-fillV_in::after {
            bottom: 0;
        }

        &.hover-fillV_out::before {
            top: 50%;
            left: 0;
            right: 0;
            height: 0;
            transform: translateY(-50%);
        }

        &.hover-fillH_in::before,
        &.hover-fillH_in::after {
            top: 0;
            bottom: 0;
            width: 0;
        }

        &.hover-fillH_in::before {
            left: 0;
        }

        &.hover-fillH_in::after {
            right: 0;
        }

        &.hover-fillH_out::before {
            top: 0;
            bottom: 0;
            left: 50%;
            width: 0;
            transform: translateX(-50%);
        }

        &:hover {
            color: v-bind('props.backgroundColor || getDefaultColors().background');

            &.hover-up::before,
            &.hover-down::before,
            &.hover-left::before,
            &.hover-right::before {
                transform: translate(0) scale(1);
            }

            &.hover-fill_out::before {
                width: 300%;
                height: 300%;
                filter: blur(1.5rem);
            }

            // &.hover-fill_in {
            //     opacity: 0.5;
            // }

            &.hover-fill_in::before {
                transform: translate(-50%, -50%) scale(0);
                opacity: 1;
                filter: blur(1.5rem);
            }

            &.hover-fillV_in::before,
            &.hover-fillV_in::after {
                height: 50%;
                filter: blur(1.5rem);
            }

            &.hover-fillV_out::before {
                height: 100%;
                filter: blur(1.5rem);
            }

            &.hover-fillH_in::before,
            &.hover-fillH_in::after {
                width: 50%;
                filter: blur(1.5rem);
            }

            &.hover-fillH_out::before {
                width: 100%;
                filter: blur(1.5rem);
            }
        }
    }
}
</style>