<template>
    <form class="create-twoot-panel" @submit.prevent="createNewTwoot" :class="{ '--exceeded': newTwootCharacterCount > 180 }">
        <label for="newTwoot"><strong>New Twoot</strong> ({{ newTwootCharacterCount }}/180)</label>
        <textarea id="newTwoot" rows="4" v-model="state.newTwoot.content" />

        <div class="create-twoot-panel__submit">
            <div class="create-twoot-type">
                <label for="newTwootType"><strong>Type: </strong></label>
                <select id="newTwootType" v-model="state.newTwoot.type">
                    <option :value="option.value" v-for="(option, index) in state.twootTypes" :key="index">
                        {{ option.name }}
                    </option>
                </select>
            </div>

            <button type="submit">Twoot!</button>
        </div>
    </form>
</template>

<script>
import { reactive, computed } from 'vue'

export default {
    name: "CreateTwootPanel",
    setup(props, context) {
        const state = reactive({
            newTwoot: {
                content: '',
                type: 'instant'
            },
            twootTypes: [
                { value: 'draft', name: 'Draft' },
                { value: 'instant', name: 'Instant Twoot' }
            ]
        })

        const newTwootCharacterCount = computed(() => state.newTwoot.content.length)

        function createNewTwoot() {
            if(state.newTwoot.content && state.newTwoot.type !== 'draft') {
                context.emit('add-twoot', state.newTwoot.content)
                state.newTwoot.content = ''
            }
        }

        return {
            state,
            newTwootCharacterCount,
            createNewTwoot
        }
    }
}
</script>

<style lang="scss" scoped>
    .create-twoot-panel {
        margin-top: 20px;
        padding: 20px 0;
        display: flex;
        flex-direction: column;

        textarea {
            border: 1px solid #dfe3e8;
            border-radius: 5px;
        }

        .create-twoot-panel__submit {
            display: flex;
            justify-content: space-between;

            .create-twoot-type {
                padding: 10px 0;
            }

            button {
                padding: 5px 20px;
                margin: auto 0;
                border-radius: 5px;
                border: none;
                background-color: deeppink;
                color: white;
                font-weight: bold;
            }
        }

        &.--exceeded {
            color: red;
            border-color: red;

            .create-twoot-panel__submit {
                button {
                    background-color: red;
                    color: white;
                }
            }
        }
    }
</style>