<script setup>
import Navbar from "../../../components/navbar.vue"
</script>

<template>

  <Navbar class="mb-5" />

  <main>
    <div id="myCarousel" class="carousel slide carousel-fade" data-bs-ride="carousel">
      <div class="carousel-indicators">
        <button
          type="button"
          data-bs-target="#myCarousel"
          data-bs-slide-to="0"
          class="active"
          aria-current="true"
          aria-label="Slide 1"
        ></button>
        <button
          type="button"
          data-bs-target="#myCarousel"
          data-bs-slide-to="1"
          aria-label="Slide 2"
        ></button>
        <button
          type="button"
          data-bs-target="#myCarousel"
          data-bs-slide-to="2"
          aria-label="Slide 3"
        ></button>
      </div>
      <div class="carousel-inner">
        <div class="carousel-item active">
          <img src="../../../assets/img/1.jpg" alt="" />
          <div class="grad"></div>

          <div class="container">
            <div class="carousel-caption text-start col-md-4">
              <h4>Picture 1</h4>
              <p class="lead">
                Cras justo odio, dapibus ac facilisis in, egestas eget quam.
                Donec id elit non mi porta gravida at eget metus. Nullam id
                dolor id nibh ultricies vehicula ut id elit.
              </p>
            </div>
          </div>
        </div>
        <div class="carousel-item">
          <img src="../../../assets/img/2.jpg" alt="" />
          <div class="grad"></div>

          <div class="container">
            <div class="carousel-caption text-start col-md-4">
              <h4>Picture 2</h4>
              <p class="lead">
                Cras justo odio, dapibus ac facilisis in, egestas eget quam.
                Donec id elit non mi porta gravida at eget metus. Nullam id
                dolor id nibh ultricies vehicula ut id elit.
              </p>
            </div>
          </div>
        </div>
        <div class="carousel-item">
          <img src="../../../assets/img/3.jpg" alt="" />
          <div class="grad"></div>

          <div class="container">
            <div class="carousel-caption text-start col-4">
              <h4>Picture 3</h4>
              <p class="lead">
                Cras justo odio, dapibus ac facilisis in, egestas eget quam.
                Donec id elit non mi porta gravida at eget metus. Nullam id
                dolor id nibh ultricies vehicula ut id elit.
              </p>
            </div>
          </div>
        </div>
      </div>
      
    </div>

    <div class="w-100 bg-body-secondary p-3">
      <h1 class="text-center">
        Destinations
      </h1>
      <div class="d-flex justify-content-center">
        <p class="lead col-6 text-center">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Maiores harum voluptatum perferendis necessitatibus labore consequatur in minima, voluptas error odit!
        </p>
      </div>

      <div class="container-lg mt-3">
        <div class="row row-cols-3">
          <div class="col">
            <div class="card">
              <img src="../../../assets/img/4.jpg" alt="image" class="card-img-top">
              <div class="card-body">
                <div class="card-title">
                  <h5>Destination 1</h5>
                  <p class="lead">
                    Lorem ipsum dolor sit, amet consectetur adipisicing elit. Laborum...
                  </p>
                </div>
              </div>
            </div>
          </div>
          <div class="col">
            <div class="card">
              <img src="../../../assets/img/5.jpg" alt="image" class="card-img-top">
              <div class="card-body">
                <div class="card-title">
                  <h5>Destination 2</h5>
                  <p class="lead">
                    Lorem ipsum dolor sit, amet consectetur adipisicing elit. Laborum...
                  </p>
                </div>
              </div>
            </div>
          </div>
          <div class="col">
            <div class="card">
              <img src="../../../assets/img/6.jpg" alt="image" class="card-img-top">
              <div class="card-body">
                <div class="card-title">
                  <h5>Destination 3</h5>
                  <p class="lead">
                    Lorem ipsum dolor sit, amet consectetur adipisicing elit. Laborum...
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.carousel {
  margin-bottom: 0rem;
}

.carousel-caption {
  bottom: 3rem;
  z-index: 10;
  left: 8%;
}

.carousel-item {
  height: 20rem;
}

.carousel-item > img {
  position: absolute;
  top: 0;
  left: 0;
  min-width: 100%;
  height: 20rem;
  object-fit: cover;
  object-position: center;
  filter: brightness(70%);
}

.grad {
  position: absolute;
  top: 0;
  left: 0;
  min-width: 100%;
  height: 32rem;
  background: rgb(0,0,0);
background: linear-gradient(
    90deg, 
    rgba(0,0,0,1) 10%, 
    rgba(0,212,255,0) 43%
  );
}

@media (min-width: 40em) {
  .carousel-caption p {
    margin-bottom: 1.25rem;
    font-size: 1.25rem;
    line-height: 1.4;
  }
}
</style>
