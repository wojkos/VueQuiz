<template>
    <div class="container-fluid">
        <br><br>
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1 class="text-center">The Vue Quiz</h1>
                
            </div>
        </div>
        <hr>
        <div class="row" style="height:250px; display: block;">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <transition name="flip" mode="out-in">
                    <component :is="mode" @answered="answered($event)" @confirmed="mode = 'app-question'"></component>
                </transition>
            </div>
        </div>
        <div class="row">
            <div class="col-xs-6 col-xs-offset-3 col-sm-8 col-sm-offset-2 col-md-2 col-md-offset-5">
                <div class="panel panel-primary">
                    <div class="panel-heading">
                        <h3 class="panel-title text-center">Your score</h3>
                    </div>
                    <div class="panel-body">
                        <h2 class="text-center">{{ counter }}</h2>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Question from './components/Question.vue';
    import Answer from './components/Answer.vue';

    export default {
        data() {
            return {
                mode: 'app-question',
                counter: 0
            }
        },
        methods: {
          answered(isCorrect) {
              if (isCorrect) {
                  this.mode = 'app-answer';
                  this.counter++;
              } else {
                  this.mode = 'app-question';
                  alert('Wrong, try again!');
              }
          }
        },
        components: {
            appQuestion: Question,
            appAnswer: Answer
        }
    }
</script>

<style>
    /* .flip-enter {
        transform: rotateY(0deg);
    } */
    .flip-enter-active {
        animation: flip-in 0.5s ease-out forwards;
    }
    /* .flip-leave {
        transform: rotateY(0deg);
    } */
    .flip-leave-active {
        animation: flip-out 0.5s ease-out forwards;
    }
    @keyframes flip-out {
        from {
            transform: rotateY(0deg);
        }
        to {
            transform: rotateY(90deg);
        }
    }

    @keyframes flip-in {
        from {
            transform: rotateY(90deg);
        }
        to {
            transform: rotateY(0deg);
        }
    }
</style>
