<script setup lang="ts" >

   const currentYear = new Date().getFullYear();


</script>



<template>
    <v-footer app>
        <v-container>
            <v-row align="center">
                <v-col cols="12" md="6" align="center" class="mb-3">
                    <span>&copy; {{ currentYear }} Your Company</span>
                </v-col>
                <v-col cols="12" md="6" align="center">
                    <v-row justify="center">
                        <v-btn icon href="#">
                            <v-icon>mdi-facebook</v-icon>
                        </v-btn>
                        <v-btn icon href="#">
                            <v-icon>mdi-twitter</v-icon>
                        </v-btn>
                        <v-btn icon href="#">
                            <v-icon>mdi-instagram</v-icon>
                        </v-btn>
                        <v-btn icon href="#">
                            <v-icon>mdi-linkedin</v-icon>
                        </v-btn>
                    </v-row>
                </v-col>
            </v-row>
        </v-container>
    </v-footer>
</template>



<style scoped>
/* Add your custom styles here */
</style>