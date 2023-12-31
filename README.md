# reactive-menu-item

## demo
https://simpleoo0o.github.io/reactive-menu-item-demo

## 安装
```shell
npm i reactive-menu-item
```

## 使用
### 基础用法
```vue
<script setup>
    // import ReactiveMenuItem from 'reactive-menu-item/ReactiveMenuItem.vue'
    // import useReactiveMenu from 'reactive-menu-item/useReactiveMenu'
    import { ReactiveMenuItem, useReactiveMenu } from 'reactive-menu-item'

    import menus from '@/menus' // 导航数据，类型为ReactiveMenuItemVO[]

    const reactiveMenuData = useReactiveMenu(menus)
</script>

<template>
    <el-container>
        <el-header>
            <div class="logo">LOGO</div>
            <el-menu
              :default-active="reactiveMenuData.topActiveIndex"
              mode="horizontal">
                <reactive-menu-item v-for="item of reactiveMenuData.menus" :key="item.id" :data="item"/>
            </el-menu>
        </el-header>
        <el-container>
            <el-aside width="200px">
                <el-menu
                  :default-active="reactiveMenuData.activeIndex"
                  mode="vertical">
                    <reactive-menu-item v-for="item of reactiveMenuData.secondMenus" :key="item.id" :data="item">
                    </reactive-menu-item>
                </el-menu>
            </el-aside>
            <el-container>
                <el-main>
                    <RouterView/>
                </el-main>
            </el-container>
        </el-container>
    </el-container>
</template>
```

### 插槽
```vue

<template>
    <el-menu
      :default-active="reactiveMenuData.activeIndex"
      mode="vertical">
        <reactive-menu-item v-for="item of reactiveMenuData.secondMenus" :key="item.id" :data="item">
            <template #menu-item="{data}">
                {{data.name}}
            </template>
            <template #menu-item-group="{data}">
                {{data.name}}
            </template>
            <template #sub-menu="{data}">
                {{data.name}}
            </template>
        </reactive-menu-item>
    </el-menu>
</template>
```

### mock
```vue
<script setup>
    // import useReactiveMenu from 'reactive-menu-item/useReactiveMenu'
    import { useReactiveMenu } from 'reactive-menu-item'

    import menus from '@/menus'

    const reactiveMenuData = useReactiveMenu(menus, {
        mock: {
            kgName: 'abc'
        }
    })
</script>
```
### 配置项
```vue
<script setup>
    // import useReactiveMenu from 'reactive-menu-item/useReactiveMenu'
    import { useReactiveMenu } from 'reactive-menu-item'

    import menus from '@/menus'

    const reactiveMenuData = useReactiveMenu(menus, {
        config: {
            autoIndex: true, // 无匹配导航时是否重定向到首页，默认true
            selfJump: false // 点击当前导航时，是否跳转，默认false
        }
    })
</script>
```

### provide
```vue
<script setup>
import { inject } from 'vue'
const reactiveMenuData = inject('reactiveMenuData')
</script>
```
