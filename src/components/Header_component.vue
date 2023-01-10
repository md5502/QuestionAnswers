<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark" style="margin-bottom: 10px;">
        <div class="container">

            <p class="navbar-brand my-auto">Questions and answers</p>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarColor01"
                aria-controls="navbarColor01" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarColor01">
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item">
                        <p  class="nav-link my-auto ">Question {{ correctCount}}/<span>{{totalCount }}</span></p>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>

<script>
export default {
    props:{
        correctCount : Number,
        totalCount: Number,
        
    }
}
</script>