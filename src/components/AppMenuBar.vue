<template>
    <div>
        <!--Nav Drawer-->
        <v-navigation-drawer app v-model="drawer" temporary>
            <v-list>
                <v-list-subheader>
                    <v-btn prepend-icon="mdi-menu" @click.stop="drawer = !drawer">
                        {{ titleBar }}
                    </v-btn>
                </v-list-subheader>
                <v-list-item v-for="(item, i) in items" :key="i" :value="item" color="primary" :href="item.href">
                    <!--
                    <template v-slot:prepend>
                        <v-icon :icon="item.icon"></v-icon>
                    </template>
<v-list-item-title v-text="item.text"></v-list-item-title>
-->

                    <v-list-item-title v-text="item.text">
                    </v-list-item-title>

                    <!--
                    <v-btn prepend-icon="mdi-pencil" :to="'/pengaturan'">{{item.text}}</v-btn>
                    -->
                </v-list-item>

            </v-list>

        </v-navigation-drawer>
        <!--Navbar-->
        <v-app-bar :elevation="2">
            <template v-slot:prepend>
                <v-app-bar-nav-icon @click.stop="drawer = !drawer" :class="{ 'shifted': drawer }"></v-app-bar-nav-icon>
            </template>

            <v-app-bar-title>{{ titleBar }}</v-app-bar-title>

            <template v-slot:append>
                <v-btn icon="mdi-bell"></v-btn>
                <div>
                    <v-menu>
                        <template v-slot:activator="{ props }">
                            <v-btn icon="mdi-account" v-bind="props"></v-btn>
                        </template>
                        <v-list>
                            <v-list-item>
                                <template v-slot:prepend>
                                    <v-icon icon="mdi-account"></v-icon>
                                </template>
                                <v-list-item-title>{{ user.name }}</v-list-item-title>
                            </v-list-item>
                            <v-list-item>
                                <template v-slot:prepend>
                                    <v-icon icon="mdi-security"></v-icon>
                                </template>
                                <v-list-item-title>{{ user.roles }}</v-list-item-title>
                            </v-list-item>
                            <v-list-item>
                                <v-list-item-title>
                                    <v-btn prepend-icon="mdi-exit-to-app" width="100%" color="red-darken-3">
                                        Logout
                                    </v-btn>
                                </v-list-item-title>
                            </v-list-item>
                        </v-list>
                    </v-menu>
                </div>
            </template>
        </v-app-bar>
    </div>

</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router';
const route = useRoute();

const titleBar = ref('DASHBOARD')

onMounted(() => {
    let path = route.path.split('/')[1];
    if (path === '') {
        titleBar.value = 'DASHBOARD'
    } else {
        titleBar.value = path.toUpperCase()
    }
});



const user = ref({
    'username': 'username',
    'name': 'I Putu Ryan Brayoga',
    'roles': 'Admin',
    'roles_code': '1'
})

const drawer = ref(null)

const items = [
    { text: 'Dashboard', icon: 'mdi-chart-bar', href: "/" },
    { text: 'Deteksi', icon: 'mdi-sine-wave', href: "/deteksi" },
    { text: 'Pengaturan', icon: 'mdi-cog', href: "/pengaturan" },
]


</script>