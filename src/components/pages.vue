<template>

    <div class="vsp-pagination__pages">
        <arrow
            v-if="withSideArrows"
            type="prev"
            class="transparent"
            :isDisabled="page === 1"
            :color="color"
            @click.native="page > 1 ? $emit('to', page - 1) : null">
        </arrow>


        <div class="vsp-pagination__pages__page"
             v-for="(p,k) in previous"
             :key="`prev_${k}`"
             :style="{color}"
             @click="$emit('to', p)">
            {{p}}
        </div>

        <div :style="{background: color}" class="vsp-pagination__pages__page is-active">{{ page }}</div>

        <div class="vsp-pagination__pages__page"
             v-for="(p,k) in next"
             :key="`next_${k}`"
             :style="{color}"
             @click="$emit('to', p)">
            {{p}}
        </div>


        <arrow
            v-if="withSideArrows"
            type="next"
            class="transparent"
            :isDisabled="page === pages"
            :color="color"
            @click.native="page < pages ? $emit('to', page + 1) : null">
        </arrow>

    </div>

</template>

<script>

    import Arrow from './../misc/arrow'

    const props = {
        page: {
            type: Number,
            default: null
        },

        pages: {
            type: Number,
            default: null
        },

        previous: {
            type: Array,
            default: []
        },

        next: {
            type: Array,
            default: []
        },

        color: {
            type: String,
            default: null
        },

        withSideArrows: {
            type: Boolean,
            default: true,
        }

    };

    export default {
        props,
        components: {Arrow}
    }


</script>
<style scoped lang="scss">

    $color-accent: #eaeaea;

    .vsp-pagination {
        &__pages {
            display: flex;
            width: auto;
            min-height: 30px;
            border-radius: 3px;
            justify-content: center;
            user-select: none;

            &__page {
                width: 30px;
                background: white;
                border-radius: 3px;
                display: flex;
                justify-content: center;
                align-items: center;
                color: #a8a8a8;
                font-size: 13px;
                margin: 0 2px;
                cursor: pointer;
                transition: .2s ease;
                border: 1px solid transparent;
                box-sizing: border-box;
                user-select: none;

                &:hover {
                    color: $color-accent;
                }

                &.prev {
                    margin-right: 5px;
                }

                &.next {
                    margin-left: 5px;
                }

                &.is-active {
                    background: $color-accent;
                    color: white;

                }

                &.is-disabled {
                    background: #eaeaea;
                    cursor: not-allowed;

                    svg {
                        fill: #a8a8a8 !important;
                    }
                }
            }
        }

    }

</style>
