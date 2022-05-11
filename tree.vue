<template>
      <div class="prime__inputFlex">
            <div v-for="(el, index) in dataElement" :key="index">
                <div
                @click="toggle(el.condition)"
                class="prime__row"
                >
                <h4 class="prime__subtile">{{el.title}}</h4>
                <span>[{{ isFolder && isOpen === el.condition ? '-' : '+' }}]</span>
                </div>
                <ul v-if="isFolder && isOpen === el.condition">
                    <div v-if="el.condition === 'régionale'">
                        <Regional :condition="el.condition"/>
                    </div>
                    <div v-if="el.condition === 'communale'">
                        <Communale/>
                    </div>
                </ul>
            </div>
      </div>
</template>
<script>
import Regional from "./Procedure/Regional.vue";
import Communale from "./Procedure/Communale.vue";

const dataElement = [
 {
     title: "Prime régionale",
     condition: "régionale"
 },
 {
     title: "Prime communale (Complémentaire)",
     condition: "communale"
 },
]
  export default {
    props: {
        prime: {
            type: Object,
            default: null,
        }
    },
    data: function () {
        return {
            dataElement,
            isOpen: "",
            isFolder: false,
        };
    },
    methods: {
        toggle: function (type) {
            this.isOpen = type;
            if (this.isOpen === type) {
                this.isFolder = !this.isFolder;
            }
        },
    },
    components: { Regional, Communale }
}
</script>
