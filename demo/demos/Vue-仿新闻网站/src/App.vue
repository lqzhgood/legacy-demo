<template>
    <div id="app">
        <loading v-show='loading'></loading>
        <NavHeader v-show='headShow'></NavHeader>
    
        <transition name="slide-down" :enter='enter' class='gagaga'>
            <keep-alive>
                <router-view class="router-view"></router-view>
            </keep-alive>
        </transition>
    
        <FooterView v-show='footerShow'></FooterView>
    </div>
</template>


<script>
import NavHeader from './components/Nav.vue'
import FooterView from './components/Footer.vue'

import Home from './components/Home.vue'

import { mapGetters } from 'vuex'


export default {
    computed: mapGetters([
        'headShow',
        'loading',
        'footerShow'
    ]),
    mounted() {
        var path = this.$route.path.substring(1);
        this.headerChange(path);
        this.footerChange(path);
    }, watch: {
        $route(to, from) {
            var path = to.path.substring(1);
            this.headerChange(path);
            this.footerChange(path);
            const toDepth = to.path.split('/').length
            const fromDepth = from.path.split('/').length
            this.transitionName = toDepth < fromDepth ? 'slide-right' : 'slide-left'
        }
    },
    methods: {
        headerChange(path) {
            if (path == 'user-info' || path == 'user-reg' || path == 'user-login' || path.indexOf('article') != -1) {
                this.$store.dispatch('HeadShowFalse')
            } else {
                this.$store.dispatch('HeadShowTrue')
            }
        },
        footerChange(path) {
            if (path.indexOf('article') == -1) {
                this.$store.dispatch('FooterShowTrue');
            } else {
                this.$store.dispatch('FooterShowFalse');
            }
        }, enter(a) {
            console.log(a)
        }
    },
    components: {
        NavHeader,
        Home,
        FooterView
    }
}
</script>

<style>
.slide-up-enter-active,
.slide-up-leave-active {
    transition: all .4s cubic-bezier(0, 1.2, 1, 0.5);
    opacity: .7;
    transform: translate3d(0, 4em, 0);
}

.slide-up-enter,
.slide-up-leave-active {
    opacity: .3;
    transform: translate3d(0, 4em, 0);
}

.slide-down-enter-active,
.slide-down-leave-active {
    transition: all .4s cubic-bezier(0, 1.2, 1, 0.5);
    opacity: .7;
    transform: translate3d(0, 6em, 0);
}

.slide-down-enter,
.slide-down-leave-active {
    opacity: .1;
    transform: translate3d(0, 6em, 0);
}

.slide-left-enter-active,
.slide-left-leave-active {
    transition: all .2s cubic-bezier(0, 1.2, 1, 0.5);
    opacity: .5;
    transform: translate3d(2em, 0, 0);
}

.slide-left-enter,
.slide-left-leave-active {
    opacity: .3;
    transform: translate3d(2em, 0, 0);
}

.slide-right-enter-active,
.slide-right-leave-active {
    transition: all .4s cubic-bezier(0, 1.2, 1, 0.5);
    opacity: .5;
    transform: translate3d(5em, 0, 0);
}

.slide-right-enter,
.slide-right-leave-active {
    opacity: .3;
    transform: translate3d(5em, 0, 0);
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity .4s
}

.fade-enter,
.fade-leave-active {
    opacity: 0
}
</style>