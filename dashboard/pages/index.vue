<template>
    <section class="section">
        <b-tabs position="is-centered" size="is-medium" class="block" v-model="activeTab">
            <b-tab-item label="Overview" icon="information-variant">
                <Overview ref="overview"/>
            </b-tab-item>
            <b-tab-item label="Nan Yuan Fishball (G7)" icon="noodles">
                <!-- nanyuan.vue -->
                <Nanyuan ref="nanyuan"/>
            </b-tab-item>
            <b-tab-item label="Hai Chew Fish Soup (G6)" icon="rice">
                <!-- haichew.vue -->
                <Haichew ref="haichew"/>
            </b-tab-item>
            <b-tab-item label="Tablevision (G7)" icon="cctv">
                <!-- tablevision.vue -->
                <Tablevision ref="tablevision"/>
            </b-tab-item>
        </b-tabs>

    </section>
</template>

<script>
import Overview from '@/pages/main'
import Nanyuan from '@/pages/nanyuan'
import Haichew from '@/pages/haichew'
import Tablevision from '@/pages/tablevision'
export default {

    head() {
        return {
            title: this.title,
        }
    },

    components: {
        Overview,
        Nanyuan,
        Haichew,
        Tablevision
    },

    data() {
        
        return {
            
            title: 'Beo Crescent IoT Dashboard',
            activeTab: 0,
        }
    },

    watch: {
        activeTab: function() {
            
            console.log(this.activeTab);
            if (this.activeTab == 1) {
                // Nanyuan Fishball Stall
                this.stopAllAPI()
                this.triggerNYAPI()
            } else if (this.activeTab == 2){
                // Haichew Fish Soup
                this.stopAllAPI()
                this.triggerHCAPI()
            } else if (this.activeTab == 3) {
                // Nanyuan Fishball Stall
                this.stopAllAPI()
                this.triggerTVAPI()
            } else {
                this.stopAllAPI()
                this.triggerMainAPI()
            }
        }
    },
    mounted:function(){
        this.triggerMainAPI() //method1 will execute at pageload
    },
    methods: {
        stopAllAPI() {
            // this function helps to stop all API once the tab is inactive
            this.$refs.nanyuan.startAPIPolling(false);
            this.$refs.tablevision.startAPIPolling(false);
            this.$refs.haichew.startAPIPolling(false);
            this.$refs.overview.startAPIPolling(false);
        },
        triggerNYAPI() {
            // triggers the api polling once clicked
            this.$refs.nanyuan.startAPIPolling(true)
        },
        triggerHCAPI() {
            // triggers the api polling once clicked
            this.$refs.haichew.startAPIPolling(true)
        },
        triggerTVAPI() {
            // triggers the api polling once clicked
            // this.$refs.tablevision.startAPIPolling(true)
        },
        triggerMainAPI() {
            this.$refs.overview.startAPIPolling(true)
        }
    }
}
</script>
