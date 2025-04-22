<script lang="ts" setup>
import { ref, computed } from "vue"
import ActiveButton from "./ActiveButton.vue";

interface Extension {
    logo: string;
    name: string;
    description: string;
    isActive: boolean;
}


const extensions = ref<Extension[]>([
    {
        "logo": "./assets/images/logo-devlens.svg",
        "name": "DevLens",
        "description": "Quickly inspect page layouts and visualize element boundaries.",
        "isActive": true
    },
    {
        "logo": "./assets/images/logo-style-spy.svg",
        "name": "StyleSpy",
        "description": "Instantly analyze and copy CSS from any webpage element.",
        "isActive": true
    },
    {
        "logo": "./assets/images/logo-speed-boost.svg",
        "name": "SpeedBoost",
        "description": "Optimizes browser resource usage to accelerate page loading.",
        "isActive": false
    },
    {
        "logo": "./assets/images/logo-json-wizard.svg",
        "name": "JSONWizard",
        "description": "Formats, validates, and prettifies JSON responses in-browser.",
        "isActive": true
    },
    {
        "logo": "./assets/images/logo-tab-master-pro.svg",
        "name": "TabMaster Pro",
        "description": "Organizes browser tabs into groups and sessions.",
        "isActive": true
    },
    {
        "logo": "./assets/images/logo-viewport-buddy.svg",
        "name": "ViewportBuddy",
        "description": "Simulates various screen resolutions directly within the browser.",
        "isActive": false
    },
    {
        "logo": "./assets/images/logo-markup-notes.svg",
        "name": "Markup Notes",
        "description": "Enables annotation and notes directly onto webpages for collaborative debugging.",
        "isActive": true
    },
    {
        "logo": "./assets/images/logo-grid-guides.svg",
        "name": "GridGuides",
        "description": "Overlay customizable grids and alignment guides on any webpage.",
        "isActive": true
    },
    {
        "logo": "./assets/images/logo-palette-picker.svg",
        "name": "Palette Picker",
        "description": "Instantly extracts color palettes from any webpage.",
        "isActive": true
    },
    {
        "logo": "./assets/images/logo-link-checker.svg",
        "name": "LinkChecker",
        "description": "Scans and highlights broken links on any page.",
        "isActive": true
    },
    {
        "logo": "./assets/images/logo-dom-snapshot.svg",
        "name": "DOM Snapshot",
        "description": "Capture and export DOM structures quickly.",
        "isActive": false
    },
    {
        "logo": "./assets/images/logo-console-plus.svg",
        "name": "ConsolePlus",
        "description": "Enhanced developer console with advanced filtering and logging.",
        "isActive": true
    }
])

type FilterStatus = 'all' | 'active' | 'inactive'
const currentFilter = ref<FilterStatus>('all')

const filteredExtensions = computed(() => {
    switch (currentFilter.value) {
        case 'active':
            return extensions.value.filter(ext => ext.isActive)
        case 'inactive':
            return extensions.value.filter(ext => !ext.isActive)
        default:
            return extensions.value
    }

})

const setFilter = (filter: FilterStatus) => {
    currentFilter.value = filter
}


const removeExtension = (extensionName: string) => {
    extensions.value = extensions.value.filter(ext => ext.name !== extensionName)
}

</script>

<template>
    <div class="filter-buttons">
        <button @click="setFilter('all')" :class="['filter-btn', { 'active': currentFilter === 'all' }]">
            Todas
        </button>
        <button @click="setFilter('active')" :class="['filter-btn', { 'active': currentFilter === 'active' }]">
            Ativas
        </button>
        <button @click="setFilter('inactive')"
            :class="['filter-btn', { 'active': currentFilter === 'inactive' }]">
            Inativas
        </button>
    </div>
    <TransitionGroup name="ext" tag="div" class="extensions-container">
        <div v-for="extension in filteredExtensions" :key="extension.name" class="card">
            <div class="card-content">
                <div class="card-image">
                    <img :src="extension.logo" :alt="extension.name + ' logo'" class="image">
                </div>
                <div class="card-text">
                    <h2 class="title">{{ extension.name }}</h2>
                    <p class="description">{{ extension.description }}</p>
                </div>
            </div>
            <div class="card-actions">
                <button class="btn remove" @click="removeExtension(extension.name)">
                    Remove
                </button>
                <ActiveButton v-model="extension.isActive" />
            </div>
        </div>
    </TransitionGroup>
</template>


<style scoped>
.extensions-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 1rem;
    width: 100%;
}

.card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background-color: var(--neutral-800);
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    height: 12rem;
    width: 320px;
    overflow: hidden;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
    transform: translateY(-4px);
    box-shadow: 0 6px 16px rgba(0, 0, 0, 0.15);
}

.card-content {
    display: flex;
    padding: 12px;
    gap: 16px;
}

.card-image {
    flex-shrink: 0;
}

.image {
    width: 3rem;
    height: 3rem;
    border-radius: 8px;
    object-fit: cover;
}

.card-text {
    display: flex;
    flex-direction: column;
    gap: 8px;
    color: white;
}

.title {
    font-size: 1.1rem;
    font-weight: 600;
    color: var(--neutral-0);
    margin: 0;
}

.description {
    font-size: 0.9rem;
    color: var(--neutral-0);
    margin: 0;
    line-height: 1.4;
}

.card-actions {
    display: flex;
    justify-content: space-between;
    padding: 8px 8px;
    gap: 12px;
}

.btn {
    display: flex;
    justify-content: space-between;
    margin: .09em;
    border-radius: 12px;
    border: 1px solid var(--neutral-300);
    padding: 8px;
    background-color: #212636;
    color: var(--neutral-300);
}

.btn.remove {
    font-weight: 800;
    font-size: 14px;
}


.btn.primary:hover {
    background-color: #4338ca;
}


.btn.remove:hover {
    background-color: #e5e7eb;
}

.ext-enter-active,
.ext-leave-active {
    transition: all 0.5s ease;
}

.ext-enter-from,
.ext-leave-to {
    opacity: 0;
    transform: translateX(400px);
}

.filter-buttons {
    display: flex;
    gap: 2em;
    border-radius: 16px;
}

.btn-action {
    padding: 1em;
    font-weight: 600;
    font-size: 16px;
    border-radius: 16px;
    border: 1px solid var(--neutral-600);
    background-color: var(--neutral-800);
    color: white;
}

.filter-buttons {
    display: flex;
    gap: 8px;
    margin-bottom: 20px;
    justify-content: center;
}

.filter-btn {
    padding: 8px 16px;
    border: none;
    border-radius: 20px;
    background: #e2e8f0;
    color: #475569;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.2s ease;
}

.filter-btn.active {
    background: #3b82f6;
    /* Azul padrão para ativo */
    color: white;
    font-weight: 600;
    box-shadow: 0 2px 5px rgba(59, 130, 246, 0.3);
}

.filter-btn:nth-child(1).active {
    background: #6366f1;
}

/* Roxo para Todas */
.filter-btn:nth-child(2).active {
    background: #10b981;
}

/* Verde para Ativas */
.filter-btn:nth-child(3).active {
    background: #ef4444;
}

/* Vermelho para Inativas */

.filter-btn:hover {
    transform: translateY(-1px);
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}
</style>