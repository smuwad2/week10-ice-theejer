<script>
export default {
    // Add code if/as necessary
    // Hint: Add properties subject, entry and mood


    data() {
        return {
            imgSources: {
                Angry: '/public/assets/angry.png',
                Happy: '/public/assets/happy.png',
                Sad: '/public/assets/sad.png',

            }
        }

    },
    props: {
        mood: String
    },
    computed: {
        imgSrc() {
            if ((this.mood != "Happy") && (this.mood != "Sad") && (this.mood != "Angry")) {
                return "...";
            }
            else {
                return this.imgSources[this.mood];
            }
        }
    }
}
</script>


<template>
    <!-- TODO: add your template code here. Use boostrap card -->
    <div class="card m-3" style="width:18rem">
        <img class="card-img-top" v-bind:src="imgSrc"></img>
        <div class="card-body">
            <h5 class="card-title">
                <slot name="subject"></slot>
            </h5>
            <p class=card-text>
                <slot name="entry"></slot>
            </p>
        </div>

    </div>

</template>
