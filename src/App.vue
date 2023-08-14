<script>
import TreeView from './components/TreeView.vue';

export default {
    components: {
        TreeView,
    },
    data() {
        return {
            node: {
                id: 1,
                label: 'root',
                children: [
                    {
                        id: 2,
                        label: 'child 1',
                        children: [
                            {
                                id: 3,
                                label: 'child 1.1',
                            },
                            {
                                id: 4,
                                label: 'child 1.2',
                                children: [],
                            },
                        ],
                    },
                    {
                        id: 5,
                        label: 'child 2',
                        children: [],
                    }],
            },
            id: 5
        };
    },
    methods: {
        addFolder(node, label) {
            console.log('addFolder', node, label);
            // put your code here
            this.id++
            node.children.push({ id: this.id, label, children: [] });
            console.log(this.node);

        },
        addFile(node, label) {
            console.log('addFile', node, label);
            // put your code here
            this.id++
            node.children.push({ id: this.id, label });

        },
        deleteNode(node) {
            console.log('deleteNode', node);
            this.deleteNodeChild(this.node, node);
        },
        deleteNodeChild(parentNode, deletedNode) {
            for (let i = 0; i < parentNode.children.length; i++) {
                const currentNode = parentNode.children[i];
                if (currentNode === deletedNode) {
                    parentNode.children.splice(i, 1);
                    break;
                } else if (currentNode.children) {
                    this.deleteNodeChild(currentNode, deletedNode);
                }
            }
        },
    },
};
</script>

<template>
    <main>
        <h2>Tree View</h2>
        <TreeView :node="node" @addFolder="addFolder" @addFile="addFile" @deleteNode="deleteNode" />
    </main>
</template>

<style>
main {
    max-width: 600px;
    margin: 0 auto;
}
</style>

