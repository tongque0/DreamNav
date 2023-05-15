<template>
    <el-container>
        <el-aside class="sidebar" :class="{ open: isSidebarOpen }">
            <button class="sidebar-toggle" @click="toggleSidebar">
                <i class="el-icon-menu"></i>
            </button>
            <el-menu v-if="isSidebarOpen" :default-active="activeIndex" @select="handleSelect" background-color="#e6f7ff" text-color="#003a8c"
                active-text-color="#1890ff" class="sidebar-menu">
                <el-menu-item v-for="(category, index) in categories" :index="index.toString()" :key="index">
                    <a :href="`#${category.name}`" class="menu-item-link">
                        <div class="menu-item-card" @click="handleSelect(index)">
                            {{ category.name }}
                        </div>
                    </a>
                </el-menu-item>
            </el-menu>
        </el-aside>

        <el-main class="content">
            <div v-for="(category, index) in categories" :key="index" :id="category.name">
                <h2>{{ category.name }}</h2>
                <el-row :gutter="20">
                    <el-col v-for="(link, linkIndex) in category.links" :key="linkIndex" :span="6">
                        <el-card class="box-card" shadow="hover" @click="openLink(link.url)">
                            <div slot="header" class="clearfix">
                                <span>{{ link.name }}</span>
                            </div>
                        </el-card>
                    </el-col>
                </el-row>
            </div>
        </el-main>
    </el-container>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';

const categories = reactive([
    { name: '常用工具', links: [{ name: 'Bilibili', url: 'https://www.bilibili.com'}, { name: '链接2', url: 'http://link2.com' }, { name: '链接2', url: 'http://link2.com' }, { name: '链接2', url: 'http://link2.com' }] },
    { name: '技术学习', links: [{ name: '链接1', url: 'http://link1.com' }, { name: '链接2', url: 'http://link2.com' }, { name: '链接2', url: 'http://link2.com' }, { name: '链接2', url: 'http://link2.com' }] },
    { name: '摸鱼玩乐', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    { name: '快乐天地', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    { name: '青青草原', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    { name: '东西南北', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    { name: '天方夜谭', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    { name: '分类9', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    { name: '分类10', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    { name: '分类11', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    { name: '分类12', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    { name: '分类13', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    { name: '分类14', links: [{ name: '链接3', url: 'http://link3.com' }, { name: '链接4', url: 'http://link4.com' }] },
    // ...
]);

const activeIndex = ref('0');

const handleSelect = (index) => {
    activeIndex.value = index;
};

const openLink = (url) => {
    window.open(url, '_blank');
};

const isSidebarOpen = ref(true);

const toggleSidebar = () => {
    isSidebarOpen.value = !isSidebarOpen.value;
};
</script>

<style scoped>
.sidebar {
    position: -webkit-sticky;
    position: sticky;
    top: 0;
    height: 100vh;
    overflow-y: auto;
    transition: width 0.3s ease;
    width: 150px;  
}

.sidebar:not(.open) {
    width: 50px !important;
}

.sidebar-toggle {
    position: absolute;
    top: 10px;
    left: 10px;
    z-index: 2;
    background-color: #1890ff;
    color: #fff;
    border: none;
    border-radius: 25px;  /* 增加圆角 */
    padding: 10px 20px;  /* 增加内边距使其看起来更大 */
    cursor: pointer;
    transition: background-color 0.3s;
}

.sidebar-toggle:hover {
    background-color: #40a9ff;
}

.sidebar-toggle::after {
    content: 'close';  /* 默认显示"开" */
}

.sidebar:not(.open) .sidebar-toggle::after {
    content: 'open';  /* 当侧边栏关闭时，显示"关" */
}

.content {
    padding: 20px;
}

@media (max-width: 600px) {
    .sidebar {
        width: 80px;
    }

    .content {
        padding: 10px;
    }

    .sidebar-menu {
        display: none;
    }

    .sidebar.open .sidebar-menu {
        display: block;    }

.sidebar-toggle {
    display: block;
}
}

.box-card {
margin-bottom: 20px;
}

.sidebar-menu .el-menu-item {
background-color: #e6f7ff;
margin: 5px 0;
padding: 10px 20px;
border-radius: 4px;
transition: all 0.3s;
}

.sidebar-menu .el-menu-item:hover {
background-color: #b3d4fc;
}

.sidebar-menu .el-menu-item.is-active {
background-color: #1890ff;
color: #fff;
}

.sidebar-menu .menu-item-card {
display: flex;
justify-content: center;
align-items: center;
text-align: center;
height: 100%;
width: 100%;
cursor: pointer;
}

.sidebar-menu .menu-item-card a {
display: block;
text-align: center;
}

.menu-item-link {
display: block;
text-decoration: none;
color: inherit;
}
</style>
