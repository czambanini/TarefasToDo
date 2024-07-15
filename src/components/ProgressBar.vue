<template>
    <div>
        <div class="bar-border"><div class="bar-progress" :style="{ width: progresso + '%' }"></div></div>
    </div>
</template>
    
<script>
    export default {
        name: 'Progresso',
        props: {
            progresso: {
                type: Number,
                default: 0
            }
        }
    }
</script>

<style scopeed>
div {
    width: 100%;
    display: flex;
    justify-content: center;
}

.bar-border {
	width: 80%;
	height: 25px;
	border: 1px solid #474747;
    border-radius: 5px;
    justify-content: left;
}

.bar-progress {
    background-color: #75c366;
	height: 25px;
    border-radius: 5px;   
}
</style>