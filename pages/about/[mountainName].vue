<template>
    <div class="outer-root-div">

        <div class="loading-div">
            <div class="img-div">
                <img src="../../assets/loading.gif" alt="">


            </div>
        </div>

        <NuxtLink to="/">
            <div class="go-back-arrow">
                <div class="arrow">
    
                </div>
            </div>
        </NuxtLink>

        <div class="mountain-container">
            <div class="mountain-content">
                <div class="grid-container">

                    <!-- mountain,country and continent name -->
                    <div class="nmg">
                        <div class="names">
                            <div class="mountain-name">
                                <h1 class="mn"></h1>
                            </div>
                            <div class="country-dets">
                                <span class="mountain-country"></span>
                                <span class="mountain-continent"></span>
                            </div>

                        </div>

                        <div class="image-container">
                            <img id="mt-image" src="" alt="mountain image">
                        </div>
                    </div>
                    
                    <!-- description -->
                    <div class="description-container">
                        <div class="dc">
                            <p class="description-p"></p>
                        </div>
                    </div>
                </div>
                

            </div>
        </div>
    </div>
</template>

<script setup>
import { onBeforeMount,ref } from 'vue';


onBeforeMount(getMountainDetails)
const parameters = useRoute()
let mountain = (parameters.params.mountainName).toLowerCase()

async function getMountainDetails(){
    const response = await fetch(`https://api.nuxtjs.dev/mountains/${mountain}`)
    const data = await response.json()


    document.querySelector('.mn').textContent =data.title
    document.querySelector('.mountain-continent').textContent =data.continent
    document.querySelector('.mountain-country').textContent =data.countries[0] +','
    document.querySelector('#mt-image').src = data.image
    document.querySelector('.description-p').textContent = data.description

    document.querySelector('.loading-div').classList.add('hide-loading-div')

    document.querySelector('.mountain-container').classList.add('show-page-content')

}

</script>

<style lang="scss" scoped>

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.loading-div{
    position: absolute;
    background-color: rgb(251, 251, 251);
    top: 0;
    left: 0;
    height: 100vh;
    width: 100vw;
    .img-div{
        height: 100%;
        width: 100%;
        display: grid;
        place-items: center;
        img{
            width: 20rem;
        }
    }

}

//class to hide loading animation
.hide-loading-div{
    display: none;
    transition: all .2s ease-in-out;
}

.mountain-container{
    opacity: 0;
}
//class to show page content
.show-page-content{
    opacity: 1;
    transition: all .2s ease-in-out;
}

.go-back-arrow{
    position: absolute;
    top: 7%;
    left: 2%;
    cursor: pointer;

    .arrow {
        width: 0;
        height: 0;
        border-left: 17px solid transparent;
        border-right: 17px solid transparent;
        transform: rotate(-90deg);
        border-bottom: 17px solid rgba(23, 82, 191, 0.416);
    }
}
.outer-root-div{
    max-width: 1200px;
    margin: 4rem auto;

    .mountain-container{
        .mountain-content{
            .grid-container{
                display: grid;
                grid-template-columns: 1fr 1fr;
                align-items: center;
                
                // mountain,country and continent name
                .nmg{
                    margin: 1rem;
                    .names{
                        .mountain-name{
                            h1{

                                font-size: 3rem;
                            }
        
                        }
                        .country-dets{
                            margin-bottom: 1rem;
                            .mountain-country, .mountain-continent{
                                padding-right: .4rem; 
                            }

                        }
                    }
                    .image-container{
                        img{
                            width: 100%;

                        }
                    }
                }

                //mountain description
                .description-container{
                    margin: 1rem;
                    .dc{
                        .description-p{
                            color: black;
                        }
                    }
                }
            }
        }
    }

}

@media screen and (max-width:900px) {
    .outer-root-div .mountain-container .mountain-content .grid-container{
        grid-template-columns: 1fr;
        justify-content: center;
    }
}

</style>