<script setup lang="ts">
import {h, ref, VNode, withDirectives } from 'vue';
import {onClickOutside} from '@vueuse/core';
import ApplicationLogo from "@/Components/ApplicationLogo.vue";
import {NavigationLinks, MenuItem} from '@/helpers/navigation';
import Button from "primevue/button";
// import Avatar from 'primevue/avatar';
import Ripple from 'primevue/ripple';
import StyleClass from 'primevue/styleclass';
import {Link} from "@inertiajs/vue3";

type SidebarProp = {
    isSidebarOpen: boolean;
};
const props = defineProps<SidebarProp>();
const emit = defineEmits<{
    updatesidebar: [value: boolean]
}>()

const navlinks: MenuItem[] = NavigationLinks;

const target = ref(null)
onClickOutside(target, () => {
    emit('updatesidebar', false);
})

function makeMenuItem(menu: MenuItem, path: string, level: number) {
    const style = level > 0 ? { paddingLeft: `${16 + level * 20}px` } : {};
    const menulevel = level > 0 ? 'submenu' : 'mainmenu';

    const props = {
        href: path,
        class: 'flex items-center cursor-pointer p-3 rounded-md text-surface-700 dark:text-surface-0/80 hover:bg-surface-100 dark:hover:bg-surface-700 duration-200 transition-colors',
        // style,
        onClick() {
            emit('updatesidebar', false);
        }
    };

    if (menu.external === true) {
        Object.assign(props, {
            target: '_blank',
        });
    }

    const child: VNode[] = [];

    menu.icon !== void 0 &&
    child.push(h('i',{ class: menu.icon, }));

    child.push(h('span', { class: 'ml-2 font-medium', innerHTML: menu.title}));

    if(menu.children) {
        const itemlink = () => withDirectives(h('a',{
                class: 'flex items-center cursor-pointer p-3 rounded-md text-surface-700 dark:text-surface-0/80 hover:bg-surface-100 dark:hover:bg-surface-700 duration-200 transition-colors'
            }, [
                h('i', { class: 'pi pi-circle-fill mr-2'}),
                h('span', menu.title),
                h('i', {class: 'pi pi-chevron-down ml-auto'})]),
            [[Ripple],
                [StyleClass, {
                    selector: '@next',
                    enterClass: 'hidden',
                    enterActiveClass: 'slidedown',
                    leaveToClass: 'hidden',
                    leaveActiveClass: 'slideup'
                }]
            ]);
        return h('li', [h(itemlink), makeMenu(menu.children, level + 1)])
    } else {
        const itemlink = h(Link, props, () => child);
        return h('li', itemlink)
    }
}
function makeMenu(menu: MenuItem[], level: number): VNode {
    const ulClass = level == 0 ? 'list-none p-0 m-0 overflow-hidden' : 'list-none py-0 pl-3 pr-0 m-0 hidden overflow-y-hidden transition-all duration-400 ease-in-out';
    return h('ul',{ class: ulClass }, menu.map((item: MenuItem) => makeMenuItem(item, item.path, level)))
}

const toggleButtonNode = h(Button, { class: "lg:hidden", icon:"pi pi-arrow-left", text: true,
    onClick(event) {
        emit('updatesidebar', false)
    }
});
const appLogoNode = h(ApplicationLogo, { class: 'w-8 h-8' });
const homeRouteNode = h(Link,{ href: route('home') }, () => appLogoNode);
const toggleMenuNode = h('div', {
    class: 'flex items-center justify-between p-4 h-14'
},[homeRouteNode, toggleButtonNode]);
const menuWrapperNode = h('div', {
    class: 'flex flex-col h-full'
}, [toggleMenuNode, makeMenu(navlinks,  0)])

const sbroot = () => h('aside', {
    ref: target,
    class: ['absolute left-0 top-0 z-9999 flex bg-gray-100 h-screen w-[18rem] flex-col overflow-y-hidden duration-300 ease-linear lg:static lg:translate-x-0', {
        'translate-x-0': props.isSidebarOpen,
        '-translate-x-full': !props.isSidebarOpen
    }]
}, menuWrapperNode);
</script>
<style>
@keyframes slidedown {
    0% {
        max-height: 0;
    }
    100% {
        max-height: auto;
    }
}

@keyframes slideup {
    0% {
        max-height: 1000px;
    }
    100% {
        max-height: 0;
    }
}

.slidedown {
    animation: slidedown 0.2s ease-in-out;
}

.slideup {
    animation: slideup 0.2s cubic-bezier(0, 1, 0, 1);
}

.layout-ripple-disabled [data-pc-name='ripple'] {
    display: none !important;
}
</style>
<template>
    <sbroot />
</template>
