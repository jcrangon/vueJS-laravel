<template>

    <div class="auth-wrapper" v-if="!user">
      <div class="auth-inner">
            <div>
                <h3 >You are not logged in</h3>
            </div>
        </div>
    </div>

    <div class="top-container d-flex flex-row justify-content-around align-items-start flex-wrap text-start mt-5">   
        <CurrencyComponent/>
        <PairComponent />
    </div>
    <div v-if="user" class="top-container d-flex flex-row justify-content-center align-items-center text-start">
        <div class="w25 bg-white">
            <AdminConverter />
        </div> 
    </div>
</template>



<script>
    import { mapState } from 'vuex';
    import AdminConverter from './AdminConverter.vue';
    import PairComponent from './PairComponent.vue';
    import CurrencyComponent from './CurrencyComponent.vue';

    export default {
        name: 'HomeComponent',

        components: {
            CurrencyComponent,
            AdminConverter,
            PairComponent,
        },
        created() {
            if(!this.user) {
                this.$router.push('/login')
            }

            if(!this.curList) {
                this.$store.dispatch('getCurList')
            }
            if(!this.curPairs) {
                this.$store.dispatch('getCurPairs')
            }
        },
        // mounted() {
        //     console.log(this.curPairs)
        // },
        computed: {
            ...mapState(['user', 'curList', 'curPairs']),
            
        },
    }
</script>

<style scoped>
.top-container {
    min-height: 45vh;
    width: 100%;
}

.cur-list {
    width: 25%;
    max-width: 100%;
    max-height: 400px;
    overflow-x: hidden;
    overflow-y: auto;
}

.w25 {
    padding:15px;
    width: 25%;
    max-width: 100%;
    border-radius: 4px;
}

.wide {
    width: 35%;
}

#currencyModal {
    display: unset;
}

#currencyPairsModal {
    display: unset;
}

.calque {
    position: fixed;
    top: 0;
    left: 0;
    width:100%;
    height:100%;
    z-index:5;
    background: #00000077;
}

.big-font {
    font-size: 32px;
    font-weight: 700;
}

.rate-def {
    font-size: 40px;
    max-width: 45%;
}

.conversion-result {
    font-size: 32px;
    font-weight: 700;
}
</style>