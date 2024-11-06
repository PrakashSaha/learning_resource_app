<template>
    <base-card>
        <base-button 
        @click="setSelectedTab('StoredResources')" 
        :mode="storeButtonMode"
        >Stored Resources</base-button>
        <base-button 
        @click="setSelectedTab('AddResource')" 
        :mode="addButtonMode"
        >Add Resources</base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</template>


<script>
import StoredResources from './StoredResources.vue'
import AddResource from './AddResource.vue';
export default{
    components: {
        StoredResources,
        AddResource
    },
    data(){
        return{
            selectedTab:'StoredResources',
            storedItems: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'Official Vue.js Documentation.',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to Google...',
                    link: 'https://google.org'
                },
                {
                    id: 'facebook',
                    title: 'facebook',
                    description: 'Welcome to my facebook page....',
                    link: 'https://www.facebook.com/.org'
                }
            ]
        };
    },
    provide(){
        return{
            resources: this.storedItems,
            addResource: this.addResource,
            deleteResources: this.removeResources,
        };
    },
    computed:{
        storeButtonMode(){
            return this.selectedTab ==='StoredResources' ? null : 'flat';
        },
        addButtonMode(){
            return this.selectedTab ==='AddResource' ? null : 'flat';
        }
    },
    methods:{
        setSelectedTab(tab){
            this.selectedTab = tab;
        },
        addResource(title, description, url){
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: url
            };
            this.storedItems.unshift(newResource);
            this.selectedTab = 'StoredResources';
        },
        removeResources(id){
            const itemIndex = this.storedItems.findIndex(item => item.id === id);
            this.storedItems.splice(itemIndex, 1);
        }
    }
}
</script>