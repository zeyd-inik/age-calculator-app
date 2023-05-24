<script setup>
import { ref } from 'vue';

const userDay = ref('');
const userMonth = ref('');
const userYear = ref('');

const resultDay = ref('--');
const resultMonth = ref('--');
const resultYear = ref('--');

const isError = ref(false);

const clickHandle = () => {
    const currentYear = new Date().getFullYear();

    if (
        userDay.value === '' ||
        userMonth.value === '' ||
        userYear.value === '' ||
        userDay.value > 31 ||
        userMonth.value > 12 ||
        currentYear < userYear.value
    ) {
        isError.value = true;
        return;
    }

    isError.value = false;
    let currentDate_milliSecond = new Date().getTime();
    let userDate_milliSecond = new Date(userYear.value, userMonth.value - 1, userDay.value).getTime();
    let diff_milliSecond = currentDate_milliSecond - userDate_milliSecond;
    let diff_String = new Date(diff_milliSecond);

    resultYear.value = Math.abs(diff_String.getFullYear() - 1970);
    resultMonth.value = diff_String.getMonth();
    resultDay.value = diff_String.getDate();
};
</script>
<template>
    <div class="app">
        <main class="main">
            <section class="entries_container">
                <div class="entry">
                    <label :class="{ error: isError }" for="day">DAY</label>
                    <input :class="{ error: isError }" type="number" v-model="userDay" placeholder="DD" id="day" />
                </div>
                <div class="entry">
                    <label :class="{ error: isError }" for="mounth">MONTH</label>
                    <input :class="{ error: isError }" type="number" v-model="userMonth" placeholder="MM" id="month" />
                </div>
                <div class="entry">
                    <label :class="{ error: isError }" for="year">YEAR</label>
                    <input :class="{ error: isError }" type="number" v-model="userYear" placeholder="YYYY" id="year" />
                </div>
            </section>
            <p v-if="isError" class="error_message">Must be a valid date</p>

            <section class="divider_container">
                <div class="hr"></div>
                <div class="img_container" @click="clickHandle">
                    <img src="./assets/images/icon-arrow.svg" alt="arrow" />
                </div>
            </section>

            <section class="results">
                <div class="result">
                    <span class="line" id="year">{{ resultYear }}</span>
                    <span>years</span>
                </div>
                <div class="result">
                    <span class="line" id="months">{{ resultMonth }}</span>
                    <span>months</span>
                </div>
                <div class="result">
                    <span class="line" id="days">{{ resultDay }}</span>
                    <span>days</span>
                </div>
            </section>
        </main>
    </div>
</template>

<style lang="scss" scoped>
.app {
    background-color: $off_white;

    min-height: 100vh;
    padding: 1rem;

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    .main {
        background-color: $white;

        display: flex;
        flex-direction: column;
        gap: 2.4rem;

        width: 350px;
        padding: 2rem;

        overflow: hidden;

        border-radius: 10px 10px 30% 10px;
        @media (min-width: 1024px) {
            width: 70vw;
            padding: 1rem 4rem 1rem;
        }
        .entries_container {
            display: flex;
            justify-content: space-between;
            gap: 0.2rem;

            color: $smokey_grey;
            @media (min-width: 1024px) {
                justify-content: flex-start;
                gap: 1rem;
            }
            .entry {
                display: flex;
                flex-direction: column;
                align-items: flex-start;
                justify-content: center;
                label {
                    font-size: 12px;
                    @media (min-width: 1024px) {
                        font-size: 1rem;
                    }
                    &.error {
                        color: $light_red;
                    }
                }
                input[type='number'] {
                    /* hide  number input arrows */
                    &::-webkit-outer-spin-button,
                    &::-webkit-inner-spin-button {
                        -webkit-appearance: none;
                    }

                    width: 85px;
                    height: 52px;
                    padding-left: 0.7rem;

                    font-size: 1.2rem;

                    border-radius: 8px;
                    border: 1px solid $light_grey;
                    outline: none;
                    &.error {
                        border-color: $light_red;
                    }
                    @media (min-width: 1024px) {
                        font-size: 1rem;
                        width: 100px;
                        height: 56px;
                    }

                    &:focus {
                        outline: 1px solid $purple;
                        cursor: default !important;
                    }

                    &:hover {
                        cursor: pointer;
                    }
                }
            }
        }
        .error_message {
            color: $light_red;
            font-weight: 400;
            font-style: italic;
            font-size: 12px;
            transform: translateY(-30px);
        }
        .divider_container {
            position: relative;
            width: 100%;
            .hr {
                height: 1px;
                width: 100%;
                background-color: $light_grey;
            }
            .img_container {
                height: 60px;
                width: 60px;
                border-radius: 50%;
                background-color: $purple;

                position: absolute;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);

                display: flex;
                justify-content: center;
                align-items: center;

                transition: all 0.3s ease;

                &:hover {
                    background-color: $off_black;
                    cursor: pointer;
                }

                img {
                    width: 30px;
                }
                @media (min-width: 1024px) {
                    /*  left: 97%; */
                    transform: translate(-50%, -50%);
                    left: 100%;

                    transform: translateY(-50%, 0);
                }
            }
        }
        .results {
            font-style: italic;
            font-weight: 800;
            span {
                font-size: 3rem;
                @media (min-width: 1024px) {
                    font-size: 3.5rem;
                }
            }
            .line {
                color: $purple;
                padding-right: 0.5rem;
                @media (min-width: 1024px) {
                    padding-right: 1.5rem;
                }
            }
        }
    }
}
</style>
