<template lang="pug">
header
    .title calc
    .themes.flex
        span.up theme
        .choices
            - var themesNum = 3;
            .nums 
                - for (var i = 1; i <= themesNum; i++) 
                    span= i
            .toggle 
                input(type="range", v-model="theme", min="1", max=themesNum, @input="changeTheme")
</template>
<script>
export default {
    data() {
        return {
            theme: 1,
            themes: [
            {
                "--bodyBg": 'hsl(222, 26%, 31%)',
                "--mainColor": 'hsl(223, 31%, 20%)',
                "--screenBg": 'hsl(224, 36%, 15%)',
                "--secondColor": 'hsl(6, 63%, 50%)',
                "--secondLightColor": 'hsl(9, 93%, 67%)',
                "--secondShadowColor": 'hsl(6, 70%, 34%)',
                "--keyBg": 'hsl(30, 25%, 89%)',
                "--keyLightBg": 'hsl(0, 0%, 100%)',
                "--keyShadow": 'hsl(28, 16%, 65%)',
                "--specialKeyBg": 'hsl(225, 21%, 49%)',
                "--specialKeyLightBg": 'hsl(224, 51%, 76%)',
                "--specialKeyShadow": 'hsl(224, 28%, 35%)',
                "--textColor": 'hsl(221, 14%, 31%)',
                "--textColor2": 'hsl(0, 0%, 100%)',
                "--equalKeyColor": '#fff',
            },
            {
                "--bodyBg": 'hsl(0, 0%, 90%)',
                "--mainColor": 'hsl(0, 5%, 81%)',
                "--screenBg": 'hsl(0, 0%, 93%)',
                "--secondColor": 'hsl(25, 98%, 40%)',
                "--secondLightColor": 'hsl(25, 100%, 61%)',
                "--secondShadowColor": 'hsl(25, 99%, 27%)',
                "--keyBg": 'hsl(45, 7%, 89%)',
                "--keyLightBg": 'hsl(0, 0%, 100%)',
                "--keyShadow": 'hsl(35, 11%, 61%)',
                "--specialKeyBg": 'hsl(185, 42%, 37%)',
                "--specialKeyLightBg": 'hsl(185, 41%, 56%)',
                "--specialKeyShadow": 'hsl(185, 58%, 25%)',
                "--textColor": 'hsl(60, 10%, 19%)',
                "--textColor2": 'hsl(60, 10%, 19%)',
                "--equalKeyColor": '#fff',
            },
            {
                "--bodyBg": 'hsl(268, 75%, 9%)',
                "--mainColor": 'hsl(268, 71%, 12%)',
                "--screenBg": 'hsl(268, 71%, 12%)',
                "--secondColor": 'hsl(176, 100%, 44%)',
                "--secondLightColor": 'hsl(177, 100%, 79%)',
                "--secondShadowColor": 'hsl(177, 92%, 70%)',
                "--keyBg": 'hsl(268, 47%, 21%)',
                "--keyLightBg": 'hsl(268, 54%, 44%)',
                "--keyShadow": 'hsl(290, 70%, 36%)',
                "--specialKeyBg": 'hsl(281, 89%, 26%)',
                "--specialKeyLightBg": 'hsl(280, 56%, 44%)',
                "--specialKeyShadow": 'hsl(285, 91%, 52%)',
                "--textColor": 'hsl(52, 100%, 62%)',
                "--textColor2": 'hsl(52, 100%, 62%)',
                "--equalKeyColor": 'hsl(198, 20%, 13%)',
            },
            ]
        }
    },
    methods: {
        changeTheme() {
            let themeProperties = this.themes[this.theme - 1];
            for (let i = 0; i < Object.keys(themeProperties).length; i++) {
                let key = Object.keys(themeProperties)[i];
                document.documentElement.style.setProperty(key, themeProperties[key])
            }
        }
    }
}
</script>
<style lang="scss">
@mixin flex($justify: center, $align: center, $gap: 10px) {
  display: flex;
  justify-content: $justify;
  align-items: $align;
  gap: $gap;
}
header {
    @include flex(space-between);
    margin: 25px 0;
    .title {
        font-size: 20px;
    }
    .themes {
        font-size: 10px;
        transition: var(--transition2);
        > span {
            margin-right: 15px;
        }
        .choices {
            .nums {
            padding: 0 7px;
            @include flex(space-between);
            }
            .toggle {
            padding: 2px;
            margin-top: 3px;
            background-color: var(--mainColor);
            border-radius: 25px;
            transition: var(--transition2);
            input {
                max-width: 60px;
                accent-color: var(--secondColor);
                appearance: none;
                background-color: transparent;
                cursor: pointer;
                transition: var(--transition);
                &:hover {
                accent-color: var(--secondLightColor);
                }
            }
        }
    }
    }
    .title, 
    .themes {
        color: var(--textColor2);
    }
}
</style>