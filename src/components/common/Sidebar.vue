<template>
    <div class="sidebar">
        <el-menu
            class="sidebar-el-menu"
            :default-active="onRoutes"
            :collapse="collapse"
            background-color=#0738A7
            text-color=white
            active-text-color="white"
            unique-opened
            router
        >
            <template v-for="item in items">
                <template v-if="item.subs">
                    <el-submenu :index="item.index" :key="item.index">
                        <template slot="title">
                            <i :class="item.icon"></i>
                            <span slot="title">{{ item.title }}</span>
                        </template>
                        <template v-for="subItem in item.subs">
                            <el-submenu
                                v-if="subItem.subs"
                                :index="subItem.index"
                                :key="subItem.index"
                            >
                                <template slot="title">{{ subItem.title }}</template>
                                <el-menu-item
                                    v-for="(threeItem,i) in subItem.subs"
                                    :key="i"
                                    :index="threeItem.index"
                                >{{ threeItem.title }}</el-menu-item>
                            </el-submenu>
                            <el-menu-item
                                v-else
                                :index="subItem.index"
                                :key="subItem.index"
                            >{{ subItem.title }}</el-menu-item>
                        </template>
                    </el-submenu>
                </template>
                <template v-else>
                    <el-menu-item :index="item.index" :key="item.index">
                        <i :class="item.icon"></i>
                        <span slot="title">{{ item.title }}</span>
                    </el-menu-item>
                </template>
            </template>
        </el-menu>
    </div>
</template>

<script>
import bus from '../common/bus';
export default {
    data() {
        return {
            collapse: false,
            items: [
                {
                    icon: 'el-icon-lx-home',
                    index: 'home',
                    title: '????????????'
                },
                {
                    icon: 'el-icon-folder-opened',
                    index: 'resourceManagement',
                    title: '????????????'
                },
                {
                    icon: 'el-icon-lx-people',
                    index: 'humancomputing',
                    title: '??????????????????'
                },
                {
                    icon: 'el-icon-s-data',
                    index: 'computingstatus',
                    title: '??????????????????'
                },
                {
                    icon: 'el-icon-finished',
                    index: 'computingresult',
                    title: '??????????????????'
                },
                // {
                //     icon: 'el-icon-lx-cascades',
                //     index: 'table',
                //     title: '????????????'
                // },
                // {
                //     icon: 'el-icon-lx-copy',
                //     index: 'tabs',
                //     title: '????????????'
                // },
                // {
                //     icon: 'el-icon-lx-calendar',
                //     index: '3',
                //     title: '????????????',
                //     subs: [
                //         {
                //             index: 'form',
                //             title: '????????????'
                //         },
                //         {
                //             index: 'upload',
                //             title: '????????????'
                //         },
                //         {
                //             index: '3-2',
                //             title: '????????????',
                //             subs: [
                //                 {
                //                     index: 'editor',
                //                     title: '??????????????????'
                //                 },
                //                 {
                //                     index: 'markdown',
                //                     title: '??????????????????'
                //                 }
                //             ]
                //         },

                //     ]
                // },

                /* {
                    icon: 'el-icon-lx-emoji',
                    index: 'icon',
                    title: '???????????????'
                }, */
                /* {
                    icon: 'el-icon-rank',
                    index: '6',
                    title: '????????????',
                    subs: [
                        {
                            index: 'drag',
                            title: '????????????'
                        },
                        {
                            index: 'dialog',
                            title: '????????????'
                        }
                    ]
                }, */
                /* {
                    icon: 'el-icon-lx-global',
                    index: 'i18n',
                    title: '???????????????'
                }, */
                {
                    icon: 'el-icon-lx-warn',
                    index: '7',
                    title: '????????????',
                    subs: [
                        {
                            index: 'permission',
                            title: '????????????'
                        },
                        {
                            index: '404',
                            title: '404??????'
                        }
                    ]
                },

            ]
        };
    },
    computed: {
        onRoutes() {
            return this.$route.path.replace('/', '');
        }
    },
    created() {
        // ?????? Event Bus ??????????????????????????????????????????
        bus.$on('collapse', msg => {
            this.collapse = msg;
            bus.$emit('collapse-content', msg);
        });
    }
};
</script>

<style scoped>
.sidebar {
    display: block;
    position: absolute;
    left: 0;
    top: 70px;
    bottom: 0;
    overflow-y: scroll;
}
.sidebar::-webkit-scrollbar {
    width: 0;
}
.sidebar-el-menu:not(.el-menu--collapse) {
    width: 250px;
}
.sidebar > ul {
    height: 100%;
}
</style>
