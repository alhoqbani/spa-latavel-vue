<template>
    <div class="container">
        <div class="columns">
            <div class="column">
                <div class="message" v-for="status in statuses">
                    <div class="message-header">
                        <p>
                            {{ status.user.name}} said...
                        </p>

                        <p>
                            {{ status.created_at | ago}}
                        </p>
                    </div>
                    <div class="message-body" v-text="status.body">

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import moment from 'moment';
    export default {
        data() {
            return {
                statuses: [],
            }
        },
        created() {
            axios.get('/statuses').
            then(({data}) => this.statuses = data)
        },

        filters: {
            ago(date) {
                return moment(date).fromNow();
            }
        }
    }
</script>
