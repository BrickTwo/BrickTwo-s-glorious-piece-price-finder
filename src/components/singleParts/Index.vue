<template>
    <b-container fluid="xl">
        <b-row>
            <b-col class="p-0" cols="3" sm="4" md="3">
                <Sidemenu class="cat" />
            </b-col>
            <b-col class="p-0" cols="9" sm="8" md="9">
                <BrickFilter class="cat" />
            </b-col>
        </b-row>
    </b-container>
</template>

<style scoped>
.cat {
    height: calc(100vh - 85px);
    min-height: 475px;
    overflow: scroll;
    overflow-x: hidden;
}
</style>

<script>
import Sidemenu from './Sidemenu';
import BrickFilter from './Filter';

export default {
    components: {
        Sidemenu,
        BrickFilter,
    },
};
</script>
