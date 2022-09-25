<template>
    <span>
        <v-navigation-drawer app v-model="drawer" dark style="border: solid 2px">
            <v-list>
                <v-list-item link to='/'>
                    <v-list-item-content>Home</v-list-item-content>
                </v-list-item>
                <v-list-item link to='/about'>
                    <v-list-item-content>About</v-list-item-content>
                </v-list-item>    
            </v-list>
        </v-navigation-drawer>

        <v-app-bar app color="blue darken-4" dark style="border: solid 2px">
            <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
        </v-app-bar>    
    </span>
</template>

<script>
export default {
    name: 'AppNavigation',
    data(){
        return {
            drawer: false,
        }
    }
}
</script>