<script>
    import Background from '$lib/images/bground.jpg'
    import BackgroundLowRes from '$lib/images/bground_lowres.jpg'

    let imageLoaded = false;

    function handleImageLoad() {
        imageLoaded = true;
    }
</script>

<div class="background-container">
    <div
            class="background-image low-res"
            style="background-image: url({BackgroundLowRes});"
            use:handleImageLoad>
    </div>

    <div
            class="background-image high-res {imageLoaded ? 'loaded' : ''}"
            style="background-image: url({Background});"
            onload={handleImageLoad}>
    </div>
</div>

<style>
    .background-container {
        position: absolute;
        width: 100vw;
        height: 100vh;
        z-index: -9;
    }

    .background-image {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        transition: opacity 0.5s;

        background-repeat: no-repeat;
        background-size: cover; /* Ensures image covers the entire element */
        background-position: center; /* Centers the image */
    }

    .background-image.low-res {
        z-index: -10;
        opacity: 0.5; /* Initial reduced opacity for the low-res image */
    }

    .background-image.high-res {
        z-index: -9;
        opacity: 0; /* Initially hidden */
    }

    .background-image.high-res.loaded {
        opacity: 1; /* Show when loaded */
    }
</style>
