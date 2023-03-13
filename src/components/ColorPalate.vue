<script setup>
import { ref, onUpdated } from "vue";
const input = ref("");
const rootColor = ref("");
const palate1 = ref("");
const palate2 = ref("");
const palate3 = ref("");
const palate4 = ref("");

/**
 * description :- onUpdated (lifecyle method for composition API)
 * created_at  :- 07/03/2023 16:10:54
 */
onUpdated(() => {
    let hex = input?.value;
    makingColorScheme(hex);
});

/**
 * description :- copyClipboard
 * created_at  :- 13/03/2023 12:10:57
 */
const copyClipboard = (text) => {
    navigator.clipboard.writeText(text);
    alert(`Copied - ${text}`);
};

/**
 * description :- makingRgb
 * created_at  :- 07/03/2023 16:33:48
 */
const makingColorScheme = (hex) => {
    const { h, s, l } = hexToHSL(hex);
    const a = 1;
    let r = `hsla(${h}, ${s}%, ${l}%, ${a})`;
    let p1 = `hsla(${h - 75}, ${s + 75}%, ${l}%, ${a})`;
    let p2 = `hsla(${h + 50}, ${s + 50}%, ${l}%, ${a})`;
    let p3 = `hsla(${h + 150}, ${s + 150}%, ${l}%, ${a})`;
    let p4 = `hsla(${h - 50}, ${s - 50}%, ${l}%, ${a})`;
    rootColor.value = r;
    palate1.value = p1;
    palate2.value = p2;
    palate3.value = p3;
    palate4.value = p4;
};

/**
 * description :- makingColorShade
 * created_at  :- 13/03/2023 10:19:39
 */
const makingColorShade = (color) => {
    let slicedVal = color.slice(5, -2);
    let c = [];
    for (let i = 1; i <= 10; i++) c.push({ color: `hsla(${slicedVal} ${i === 10 ? i : "." + i})` });
    return c;
};

/**
 * description :- hexToHSL
 * created_at  :- 07/03/2023 17:22:21
 */
const hexToHSL = (hex) => {
    const result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hex);
    let r = parseInt(result[1], 16);
    let g = parseInt(result[2], 16);
    let b = parseInt(result[3], 16);

    (r /= 255), (g /= 255), (b /= 255);
    let max = Math.max(r, g, b),
        min = Math.min(r, g, b);
    let h,
        s,
        l = (max + min) / 2;

    if (max == min) {
        h = s = 0; // achromatic
    } else {
        var d = max - min;
        s = l > 0.5 ? d / (2 - max - min) : d / (max + min);
        switch (max) {
            case r:
                h = (g - b) / d + (g < b ? 6 : 0);
                break;
            case g:
                h = (b - r) / d + 2;
                break;
            case b:
                h = (r - g) / d + 4;
                break;
        }

        h /= 6;
    }

    h = Math.round(h * 360);
    s = Math.round(s * 100);
    l = Math.round(l * 100);
    return { h, s, l };
};
</script>

<template>
    <div id="colorPalate" class="mt-4">
        <div class="form-group">
            <label class="mb-1">Choose Color </label>
            <span :style="{ color: rootColor }"> : {{ rootColor }}</span>
            <div class="color-group row">
                <div class="col-5">
                    <input class="form-control form-control-lg p-1 rounded-0" :style="{ 'border-color': input }" type="color" v-model="input" />
                </div>
                <div class="col block">
                    <ul v-if="rootColor" class="list-unstyled d-flex">
                        <li v-if="rootColor" class="p-4" :style="{ 'background-color': rootColor }"></li>
                        <li v-if="palate1" class="p-4" :style="{ 'background-color': palate1 }"></li>
                        <li v-if="palate2" class="p-4" :style="{ 'background-color': palate2 }"></li>
                        <li v-if="palate2" class="p-4" :style="{ 'background-color': palate3 }"></li>
                        <li v-if="palate2" class="p-4" :style="{ 'background-color': palate4 }"></li>
                    </ul>
                </div>
            </div>
            <div class="color-group mt-3">
                <ul v-if="rootColor" class="list-unstyled d-flex flex-row-reverse justify-content-end m-1">
                    <li
                        v-for="item in makingColorShade(rootColor)"
                        @click="copyClipboard(item.color)"
                        :style="{ 'background-color': item.color }"
                        class="p-4 px-5 position-relative"
                    >
                        <span class="d-inline-block position-absolute top-50 start-50 translate-middle">Copy</span>
                    </li>
                </ul>
                <ul v-if="palate1" class="list-unstyled d-flex flex-row-reverse justify-content-end m-1">
                    <li
                        v-for="item in makingColorShade(palate1)"
                        @click="copyClipboard(item.color)"
                        :style="{ 'background-color': item.color }"
                        class="p-4 px-5 position-relative"
                    >
                        <span class="d-inline-block position-absolute top-50 start-50 translate-middle">Copy</span>
                    </li>
                </ul>
                <ul v-if="palate2" class="list-unstyled d-flex flex-row-reverse justify-content-end m-1">
                    <li
                        v-for="item in makingColorShade(palate2)"
                        @click="copyClipboard(item.color)"
                        :style="{ 'background-color': item.color }"
                        class="p-4 px-5 position-relative"
                    >
                        <span class="d-inline-block position-absolute top-50 start-50 translate-middle">Copy</span>
                    </li>
                </ul>
                <ul v-if="palate3" class="list-unstyled d-flex flex-row-reverse justify-content-end m-1">
                    <li
                        v-for="item in makingColorShade(palate3)"
                        @click="copyClipboard(item.color)"
                        :style="{ 'background-color': item.color }"
                        class="p-4 px-5 position-relative"
                    >
                        <span class="d-inline-block position-absolute top-50 start-50 translate-middle">Copy</span>
                    </li>
                </ul>
                <ul v-if="palate4" class="list-unstyled d-flex flex-row-reverse justify-content-end m-1">
                    <li
                        v-for="item in makingColorShade(palate4)"
                        @click="copyClipboard(item.color)"
                        :style="{ 'background-color': item.color }"
                        class="p-4 px-5 position-relative"
                    >
                        <span class="d-inline-block position-absolute top-50 start-50 translate-middle">Copy</span>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>
