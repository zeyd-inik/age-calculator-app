<script setup></script>
<template>
    <div class="app">
        <main class="main">
            <section class="entries_container">
                <div class="entry">
                    <label for="day">DAY</label>
                    <input type="number" placeholder="DD" id="day" />
                </div>
                <div class="entry">
                    <label for="mounth">MONTH</label>
                    <input type="number" placeholder="MM" id="month" />
                </div>
                <div class="entry">
                    <label for="year">YEAR</label>
                    <input type="number" placeholder="YYYY" id="year" />
                </div>
            </section>
            <!-- here -->
            <section class="divider_container">
                <div class="hr"></div>
                <div class="img_container">
                    <img src="./assets/images/icon-arrow.svg" alt="arrow" />
                </div>
            </section>
            <section class="results">
                <div class="result">
                    <span class="line" id="year">--</span>
                    <span>years</span>
                </div>
                <div class="result">
                    <span class="line" id="months">--</span>
                    <span>months</span>
                </div>
                <div class="result">
                    <span class="line" id="days">--</span>
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
    padding: 1rem 0;

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    .main {
        background-color: $white;

        display: flex;
        flex-direction: column;
        gap: 3rem;

        width: 350px;
        padding: 2rem;
        overflow: hidden;

        border-radius: 5% 5% 30% 5%;
        .entries_container {
            display: flex;
            justify-content: space-between;
            gap: 0.2rem;

            color: $smokey_grey;
            .entry {
                display: flex;
                flex-direction: column;
                align-items: flex-start;
                justify-content: center;
                label {
                    font-size: 12px;
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
        .divider_container {
            position: relative;
            .hr {
                height: 1px;
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
            }
        }
        .results {
            font-style: italic;
            font-weight: 800;
            span {
                font-size: 3rem;
            }
            .line {
                color: $purple;
                padding-right: 0.5rem;
            }
        }
    }
}
</style>
