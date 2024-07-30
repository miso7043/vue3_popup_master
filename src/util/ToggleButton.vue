<template>
    <div class="btnContainer" :style="containerStyle">
        <button :class="btn_type" :style="buttonStyle" @mouseenter="handleMouseEnter" @mouseleave="handleMouseLeave">
            {{ btnTitle }}
        </button>
    </div>
</template>

<script setup>
import { computed, ref, onMounted } from 'vue';

const props = defineProps({
    btnType: {
        type: String,
        required: true
    },
    btnTitle: {
        type: String,
        default: "button"
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
    borderRadius: {
        type: String
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
    fontSize: props.fontSize,
    fontWeight: props.fontWeight,
}));

const getDefaultColors = () => {
    switch (props.btnType) {
        case 'btn-rectangle':
            return { backgroundColor: '#008CBA', color: 'white' };
        case 'btn-rounded':
            return { backgroundColor: '#4CAF50', color: 'white' };
        case 'btn-shadow':
            return { backgroundColor: 'white', color: 'black' };
        case 'btn-glass':
            return { backgroundColor: '#0000ffaa', color: 'white' };
        case 'btn-circle':
            return { backgroundColor: '#f44336', color: 'white' };
        case 'btn-icon':
            return { backgroundColor: 'yellow', color: 'black' };
        case 'btn-outline':
            return { backgroundColor: 'transparent', color: '#008CBA', border: '2px solid #008CBA' };
        case 'btn-gradient':
            return { backgroundColor: 'white', backgroundImage: 'linear-gradient(45deg, #f44336, #4CAF50)', color: 'white' };
        case 'btn-text':
            return { backgroundColor: 'transparent', color: '#4CAF50', border: '2px solid transparent' };
        case 'btn-ghost':
            return { backgroundColor: 'transparent', color: 'white', border: '2px solid yellow' };
        default:
            return { backgroundColor: '#008CBA', color: 'white' };
    }
};

const buttonStyle = computed(() => {
    const defaultColors = getDefaultColors();
    let style = {
        backgroundColor: props.backgroundColor || defaultColors.backgroundColor,
        color: props.color || defaultColors.color,
        fontWeight: props.fontWeight,
        transition: `all ${props.transitionTime}s ease`,
    };

    style = addBtnHoverColor(style);
    style = addBorderRadius(style);

    return style;
});

const addBtnHoverColor = (style) => {
    if (isHovered.value) {
        switch (props.btnType) {
            case 'btn-outline':
            case 'btn-text':
                style.background = style.color;
                style.color = 'white';
                break;
            case 'btn-ghost':
                style.background = style.color;
                style.color = 'black';
                break;

            case 'btn-gradient':
                style.backgroundClip = 'text';
                style.webkitBackgroundClip = 'text';
                style.color = 'transparent';
                style.webkitTextFillColor = 'transparent';
                style.backgroundImage = 'linear-gradient(45deg, #f44336, #4CAF50)';
                break;
            default:
                // Swap colors for non-transparent backgrounds
                [style.backgroundColor, style.color] = [style.color, style.backgroundColor];
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
    .button-rectangle {}

    /* 2. 둥근 모서리 버튼 */
    .button-rounded {}

    /* 3. 원형 버튼 */
    .button-circle {
        line-height: 50px;
        height: 120%;
        width: auto;
        aspect-ratio: 1/1;
    }

    /* 4. 아이콘 버튼 */
    .button-icon {
        padding: 10px;
    }

    /* 5. 그림자 버튼 */
    .button-shadow {
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    /* 6. 테두리 버튼 */
    .button-outline {
        border: 2px solid #008CBA;
    }

    /* 7. 유리 효과 버튼 */
    .button-glass {
        backdrop-filter: blur(10px);
    }

    /* 8. 그라디언트 버튼 */
    .button-gradient {
        background-image: linear-gradient(45deg, #f44336, #4CAF50);
    }

    /* 9. 텍스트 버튼 */
    .button-text {
        text-decoration: underline;
    }

    /* 10. 고스트 버튼 */
    .button-ghost {
        border: 2px solid white;
    }
}
</style>