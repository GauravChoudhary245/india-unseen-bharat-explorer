# india-unseen-bharat-explorer
Explore every village, town, fort &amp; temple of Bharat — Wikipedia-powered travel guide with live photos, maps &amp; stories. Search Sarangpur, UTCL Rawan, Mandu to Hampi.

web link :- 
https://travelindia-country.netlify.app

code:-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>India Unseen — Discover India Differently</title>

<meta name="description"
content="India Unseen — discover India's hidden places, heritage, landscapes and stories through Wikipedia and interactive maps.">

<!-- Leaflet -->
<link
rel="stylesheet"
href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
/>

<style>

/* =========================================================
   RESET
========================================================= */

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html{
    scroll-behavior:smooth;
}

body{
    background:#050505;
    color:#fff;
    font-family:Arial,Helvetica,sans-serif;
    overflow-x:hidden;
}

button,
input{
    font:inherit;
}

button{
    cursor:pointer;
}


/* =========================================================
   VARIABLES
========================================================= */

:root{
    --gold:#d6b36a;
    --dark:#050505;
    --panel:#101010;
    --line:rgba(255,255,255,.12);
    --muted:#999;
}


/* =========================================================
   WELCOME SCREEN
========================================================= */

#intro{
    position:fixed;
    inset:0;
    z-index:99999;

    display:flex;
    align-items:center;
    justify-content:center;

    text-align:center;

    background:#030303;

    transition:
        opacity .9s ease,
        transform .9s ease;
}

.intro-bg{
    position:absolute;
    inset:0;

    background:
        linear-gradient(
            rgba(0,0,0,.48),
            rgba(0,0,0,.82)
        ),
        url("https://images.unsplash.com/photo-1524492412937-b28074a5d7da?auto=format&fit=crop&w=2400&q=90")
        center/cover;

    animation:introZoom 10s ease forwards;
}

@keyframes introZoom{
    from{
        transform:scale(1);
    }

    to{
        transform:scale(1.12);
    }
}

.intro-content{
    position:relative;
    z-index:5;

    width:100%;
    padding:30px;

    pointer-events:auto;
}

.intro-small{
    color:var(--gold);

    font-size:11px;
    letter-spacing:7px;

    margin-bottom:25px;
}

.intro-title{
    font-family:Georgia,serif;

    font-size:
        clamp(55px,10vw,140px);

    line-height:.84;

    letter-spacing:-6px;
}

.intro-sub{
    margin-top:30px;

    color:#ccc;

    font-size:11px;
    letter-spacing:4px;
}

.enter-btn{
    position:relative;
    z-index:20;

    margin-top:45px;

    padding:16px 35px;

    color:#fff;
    background:rgba(255,255,255,.05);

    border:1px solid rgba(255,255,255,.55);

    font-size:11px;
    letter-spacing:3px;

    touch-action:manipulation;

    transition:
        background .3s ease,
        color .3s ease,
        transform .3s ease;
}

.enter-btn:hover{
    background:#fff;
    color:#000;
    transform:translateY(-3px);
}

.enter-btn:active{
    transform:scale(.97);
}


/* =========================================================
   NAVBAR
========================================================= */

nav{
    position:fixed;
    top:0;
    left:0;
    right:0;

    z-index:1000;

    display:flex;
    align-items:center;
    justify-content:space-between;

    padding:25px 5%;

    background:
        linear-gradient(
            rgba(0,0,0,.75),
            transparent
        );

    backdrop-filter:blur(5px);
}

.logo{
    font-family:Georgia,serif;

    font-size:21px;
    letter-spacing:3px;
}

.logo span{
    color:var(--gold);
}

.nav-links{
    display:flex;
    gap:30px;
}

.nav-links a{
    color:#fff;

    text-decoration:none;

    font-size:10px;
    letter-spacing:2px;

    opacity:.8;

    transition:.25s;
}

.nav-links a:hover{
    color:var(--gold);
    opacity:1;
}

@media(max-width:700px){

    .nav-links{
        display:none;
    }

}


/* =========================================================
   HERO
========================================================= */

.hero{
    min-height:100vh;

    display:flex;
    align-items:flex-end;

    padding:
        0 6%
        9%;

    position:relative;

    background:
        linear-gradient(
            180deg,
            rgba(0,0,0,.12),
            rgba(0,0,0,.25) 40%,
            #050505 100%
        ),
        url("https://images.unsplash.com/photo-1524492412937-b28074a5d7da?auto=format&fit=crop&w=2400&q=90")
        center/cover;
}

.hero-content{
    max-width:950px;
}

.hero-kicker{
    color:var(--gold);

    font-size:11px;
    letter-spacing:6px;

    margin-bottom:23px;
}

.hero h1{
    font-family:Georgia,serif;

    font-size:
        clamp(60px,10vw,145px);

    line-height:.8;

    letter-spacing:-6px;
}

.hero p{
    max-width:620px;

    margin-top:35px;

    color:#ccc;

    font-size:15px;
    line-height:1.8;
}


/* =========================================================
   SEARCH
========================================================= */

.search-area{
    padding:80px 6% 30px;

    background:#050505;
}

.search-box{
    max-width:900px;
    margin:auto;
}

.search-label{
    color:#777;

    font-size:10px;
    letter-spacing:4px;

    margin-bottom:12px;
}

.search-box input{
    width:100%;

    padding:22px 24px;

    color:#fff;
    background:#101010;

    border:1px solid var(--line);

    outline:none;

    font-size:16px;

    transition:border .25s;
}

.search-box input:focus{
    border-color:var(--gold);
}

#wikiResults{
    max-width:900px;

    margin:20px auto 0;
}

.wiki-result{
    display:flex;
    gap:18px;

    padding:15px;

    margin-bottom:10px;

    background:#0d0d0d;

    border:1px solid var(--line);

    cursor:pointer;

    transition:.25s;
}

.wiki-result:hover{
    border-color:var(--gold);
    transform:translateX(4px);
}

.wiki-result img{
    width:100px;
    height:75px;

    object-fit:cover;

    flex-shrink:0;
}

.wiki-result h3{
    font-family:Georgia,serif;

    margin-bottom:7px;
}

.wiki-result p{
    color:#999;

    font-size:13px;
    line-height:1.5;
}


/* =========================================================
   SECTIONS
========================================================= */

.section{
    padding:90px 6%;
}

.section-head{
    display:flex;
    justify-content:space-between;
    align-items:end;

    gap:30px;

    margin-bottom:40px;
}

.section-kicker{
    color:var(--gold);

    font-size:10px;
    letter-spacing:5px;

    margin-bottom:12px;
}

.section-title{
    font-family:Georgia,serif;

    font-size:
        clamp(35px,5vw,65px);

    font-weight:normal;
}

.section-description{
    max-width:450px;

    color:#888;

    font-size:14px;
    line-height:1.7;
}


/* =========================================================
   FILTERS
========================================================= */

.filters{
    display:flex;
    flex-wrap:wrap;

    gap:10px;

    margin-bottom:35px;
}

.filter{
    padding:10px 17px;

    color:#aaa;
    background:#0d0d0d;

    border:1px solid var(--line);

    font-size:10px;
    letter-spacing:2px;

    text-transform:uppercase;

    transition:.25s;
}

.filter:hover,
.filter.active{
    color:#fff;
    border-color:var(--gold);
}


/* =========================================================
   DESTINATIONS
========================================================= */

.destination-grid{
    display:grid;

    grid-template-columns:
        repeat(3,1fr);

    gap:20px;
}

@media(max-width:1000px){

    .destination-grid{
        grid-template-columns:
            repeat(2,1fr);
    }

}

@media(max-width:650px){

    .destination-grid{
        grid-template-columns:1fr;
    }

}

.destination-card{
    position:relative;

    height:500px;

    overflow:hidden;

    background:#111;

    cursor:pointer;
}

.destination-card img{
    width:100%;
    height:100%;

    object-fit:cover;

    transition:
        transform .8s ease;
}

.destination-card:hover img{
    transform:scale(1.08);
}

.destination-overlay{
    position:absolute;
    inset:0;

    display:flex;
    flex-direction:column;
    justify-content:flex-end;

    padding:28px;

    background:
        linear-gradient(
            transparent 25%,
            rgba(0,0,0,.9)
        );
}

.destination-number{
    color:var(--gold);

    font-size:10px;
    letter-spacing:3px;

    margin-bottom:10px;
}

.destination-name{
    font-family:Georgia,serif;

    font-size:35px;
}

.destination-state{
    color:#bbb;

    font-size:12px;

    margin-top:8px;
}

.destination-arrow{
    position:absolute;

    top:25px;
    right:25px;

    width:42px;
    height:42px;

    display:flex;
    align-items:center;
    justify-content:center;

    border:1px solid rgba(255,255,255,.4);

    font-size:18px;
}


/* =========================================================
   EXPERIENCE
========================================================= */

.experience{
    min-height:80vh;

    display:flex;
    align-items:center;

    padding:100px 7%;

    background:
        linear-gradient(
            90deg,
            rgba(0,0,0,.95),
            rgba(0,0,0,.3)
        ),
        url("https://images.unsplash.com/photo-1477587458883-47145ed94245?auto=format&fit=crop&w=2200&q=90")
        center/cover;
}

.experience-content{
    max-width:700px;
}

.experience h2{
    font-family:Georgia,serif;

    font-size:
        clamp(45px,7vw,90px);

    font-weight:normal;
}

.experience p{
    max-width:600px;

    margin-top:25px;

    color:#ccc;

    line-height:1.9;
}


/* =========================================================
   DESTINATION DETAILS
========================================================= */

#detailSection{
    display:none;

    padding:100px 6%;

    background:#080808;
}

.detail-grid{
    display:grid;

    grid-template-columns:
        1.1fr .9fr;

    gap:50px;

    align-items:start;
}

@media(max-width:850px){

    .detail-grid{
        grid-template-columns:1fr;
    }

}

.detail-image{
    width:100%;

    min-height:500px;

    object-fit:cover;

    background:#111;
}

.detail-kicker{
    color:var(--gold);

    font-size:10px;
    letter-spacing:5px;
}

.detail-title{
    font-family:Georgia,serif;

    font-size:
        clamp(45px,7vw,90px);

    font-weight:normal;

    line-height:.95;

    margin:20px 0;
}

.detail-location{
    color:#aaa;

    margin-bottom:25px;
}

.detail-text{
    color:#bbb;

    font-size:15px;
    line-height:1.9;
}

.wiki-button{
    display:inline-block;

    margin-top:30px;

    padding:14px 22px;

    color:#fff;

    border:1px solid var(--gold);

    text-decoration:none;

    font-size:10px;
    letter-spacing:2px;

    transition:.3s;
}

.wiki-button:hover{
    color:#000;
    background:var(--gold);
}


/* =========================================================
   WIKIPEDIA
========================================================= */

#wikipediaPanel{
    margin-top:50px;

    padding:35px;

    background:#0d0d0d;

    border:1px solid var(--line);
}

.wiki-top{
    display:flex;

    justify-content:space-between;
    align-items:center;

    gap:25px;
}

.wiki-top h2{
    font-family:Georgia,serif;

    font-size:35px;

    font-weight:normal;
}

.wiki-source{
    color:var(--gold);

    font-size:10px;
    letter-spacing:3px;
}

#wikiExtract{
    margin-top:20px;
}


/* =========================================================
   MAP
========================================================= */

.map-section{
    padding:90px 6%;

    background:#050505;
}

.map-title{
    font-family:Georgia,serif;

    font-size:45px;

    font-weight:normal;

    margin-bottom:30px;
}

#map{
    width:100%;

    height:560px;

    border:1px solid var(--line);
}


/* =========================================================
   GALLERY
========================================================= */

.gallery{
    display:grid;

    grid-template-columns:
        repeat(4,1fr);

    gap:10px;
}

.gallery img{
    width:100%;
    height:260px;

    object-fit:cover;

    background:#111;

    transition:.4s;
}

.gallery img:hover{
    transform:scale(1.02);
}

@media(max-width:800px){

    .gallery{
        grid-template-columns:
            repeat(2,1fr);
    }

}

@media(max-width:500px){

    .gallery{
        grid-template-columns:1fr;
    }

}


/* =========================================================
   FOOTER
========================================================= */

footer{
    padding:70px 6% 35px;

    background:#030303;

    border-top:1px solid var(--line);
}

.footer-logo{
    font-family:Georgia,serif;

    font-size:35px;
}

.footer-logo span{
    color:var(--gold);
}

.footer-description{
    max-width:550px;

    margin-top:15px;

    color:#777;

    line-height:1.7;
}

.footer-bottom{
    display:flex;

    justify-content:space-between;

    gap:15px;

    margin-top:70px;
    padding-top:20px;

    border-top:1px solid var(--line);

    color:#555;

    font-size:11px;
}

@media(max-width:600px){

    .footer-bottom{
        flex-direction:column;
    }

}


/* =========================================================
   LOADING
========================================================= */

.loading{
    padding:25px 0;

    color:#777;

    font-size:12px;

    letter-spacing:2px;
}


/* =========================================================
   SAFE IMAGE FALLBACK
========================================================= */

/*
   IMPORTANT:
   This is NOT a Taj Mahal image.

   If Wikipedia fails, the destination remains a
   dark cinematic panel instead of showing another
   destination's photograph.
*/

.image-fallback{
    background:
        radial-gradient(
            circle at 30% 30%,
            #3b3425,
            #151515 55%,
            #050505 100%
        ) !important;
}


/* =========================================================
   MOBILE
========================================================= */

@media(max-width:600px){

    .intro-title{
        letter-spacing:-3px;
    }

    .hero h1{
        letter-spacing:-4px;
    }

    .hero{
        padding-bottom:14%;
    }

    .detail-image{
        min-height:350px;
    }

    #map{
        height:450px;
    }

    .wiki-top{
        flex-direction:column;
        align-items:flex-start;
    }

}

</style>
</head>


<body>


<!-- =======================================================
     WELCOME SCREEN
======================================================= -->

<div id="intro">

    <div class="intro-bg"></div>

    <div class="intro-content">

        <div class="intro-small">
            A JOURNEY THROUGH INDIA
        </div>

        <div class="intro-title">
            INDIA<br>
            UNSEEN
        </div>

        <div class="intro-sub">
            STORIES • PLACES • HERITAGE
        </div>

        <button
            type="button"
            class="enter-btn"
            id="enterButton"
            onclick="enterWebsite()"
        >
            TAP TO EXPLORE
        </button>

    </div>

</div>


<!-- =======================================================
     NAVIGATION
======================================================= -->

<nav>

    <div class="logo">
        INDIA <span>UNSEEN</span>
    </div>

    <div class="nav-links">

        <a href="#destinations">
            DESTINATIONS
        </a>

        <a href="#experience">
            EXPERIENCE
        </a>

        <a href="#mapSection">
            MAP
        </a>

        <a href="#gallery">
            GALLERY
        </a>

    </div>

</nav>


<!-- =======================================================
     HERO
======================================================= -->

<section class="hero">

    <div class="hero-content">

        <div class="hero-kicker">
            DISCOVER THE OTHER SIDE OF INDIA
        </div>

        <h1>
            INDIA<br>
            UNSEEN
        </h1>

        <p>
            Go beyond the famous landmarks.
            Discover ancient cities, mountain valleys,
            forgotten architecture, living traditions
            and stories hidden across India.
        </p>

    </div>

</section>


<!-- =======================================================
     SEARCH
======================================================= -->

<section class="search-area">

    <div class="search-box">

        <div class="search-label">
            SEARCH INDIA
        </div>

        <input
            id="searchInput"
            type="text"
            placeholder="Search places, monuments, cities..."
            autocomplete="off"
        >

    </div>

    <div id="wikiResults"></div>

</section>


<!-- =======================================================
     DESTINATIONS
======================================================= -->

<section
    class="section"
    id="destinations"
>

    <div class="section-head">

        <div>

            <div class="section-kicker">
                CURATED JOURNEYS
            </div>

            <h2 class="section-title">
                Explore India
            </h2>

        </div>

        <p class="section-description">
            Explore destinations selected for their history,
            architecture, culture, landscapes and stories.
        </p>

    </div>


    <div class="filters">

        <button
            class="filter active"
            data-filter="all"
        >
            All
        </button>

        <button
            class="filter"
            data-filter="heritage"
        >
            Heritage
        </button>

        <button
            class="filter"
            data-filter="mountains"
        >
            Mountains
        </button>

        <button
            class="filter"
            data-filter="nature"
        >
            Nature
        </button>

        <button
            class="filter"
            data-filter="culture"
        >
            Culture
        </button>

    </div>


    <div
        id="destinationGrid"
        class="destination-grid"
    ></div>

</section>


<!-- =======================================================
     EXPERIENCE
======================================================= -->

<section
    class="experience"
    id="experience"
>

    <div class="experience-content">

        <div class="section-kicker">
            MORE THAN A DESTINATION
        </div>

        <h2>
            Every place<br>
            has a story.
        </h2>

        <p>
            India is not simply a collection of destinations.
            It is a collection of civilizations, landscapes,
            people, memories and stories.
            India Unseen brings those stories together.
        </p>

    </div>

</section>


<!-- =======================================================
     DESTINATION DETAIL
======================================================= -->

<section id="detailSection">

    <div class="detail-grid">

        <img
            id="detailImage"
            class="detail-image"
            alt=""
        >

        <div>

            <div
                id="detailKicker"
                class="detail-kicker"
            >
                DESTINATION
            </div>

            <h2
                id="detailTitle"
                class="detail-title"
            ></h2>

            <div
                id="detailLocation"
                class="detail-location"
            ></div>

            <div
                id="detailText"
                class="detail-text"
            ></div>

            <a
                id="wikiButton"
                class="wiki-button"
                href="#"
                target="_blank"
                rel="noopener"
            >
                READ ON WIKIPEDIA
            </a>

        </div>

    </div>


    <div id="wikipediaPanel">

        <div class="wiki-top">

            <h2>
                Wikipedia
            </h2>

            <div class="wiki-source">
                LIVE INFORMATION
            </div>

        </div>

        <div
            id="wikiExtract"
            class="detail-text"
        >
            Loading Wikipedia information...
        </div>

    </div>

</section>


<!-- =======================================================
     MAP
======================================================= -->

<section
    class="map-section"
    id="mapSection"
>

    <h2 class="map-title">
        Find the Place
    </h2>

    <div id="map"></div>

</section>


<!-- =======================================================
     GALLERY
======================================================= -->

<section
    class="section"
    id="gallery"
>

    <div class="section-head">

        <div>

            <div class="section-kicker">
                VISUAL INDIA
            </div>

            <h2 class="section-title">
                Through the Lens
            </h2>

        </div>

    </div>

    <div
        id="galleryGrid"
        class="gallery"
    ></div>

</section>


<!-- =======================================================
     FOOTER
======================================================= -->

<footer>

    <div class="footer-logo">
        INDIA <span>UNSEEN</span>
    </div>

    <p class="footer-description">
        Discover India's places, stories, heritage
        and landscapes through an interactive journey.
    </p>

    <div class="footer-bottom">

        <span>
            INDIA UNSEEN
        </span>

        <span>
            Wikipedia • OpenStreetMap • Leaflet
        </span>

    </div>

</footer>


<!-- =======================================================
     LEAFLET
======================================================= -->

<script
src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js">
</script>


<script>

/* =========================================================
   INDIA UNSEEN DATA
========================================================= */

const places = [

    {
        name:"Mandu",
        state:"Madhya Pradesh",
        category:"heritage",

        wiki:"Mandu, Madhya Pradesh",

        /*
         IMPORTANT:
         Mandu gets Hoshang Shah's Tomb.
         It does NOT get Taj Mahal.
        */
        imageWiki:"Hoshang Shah's Tomb",

        lat:22.3333,
        lng:75.4000,

        description:
        "Mandu is a historic fortified city in Madhya Pradesh known for its medieval architecture, palaces, pavilions and monuments."
    },


    {
        name:"Hampi",
        state:"Karnataka",
        category:"heritage",

        wiki:"Hampi",
        imageWiki:"Virupaksha Temple, Hampi",

        lat:15.3350,
        lng:76.4600,

        description:
        "Hampi is a UNESCO World Heritage landscape filled with temples, stone architecture, ruins and dramatic boulder-covered hills."
    },


    {
        name:"Jaipur",
        state:"Rajasthan",
        category:"heritage",

        wiki:"Jaipur",
        imageWiki:"Hawa Mahal",

        lat:26.9124,
        lng:75.7873,

        description:
        "Jaipur is Rajasthan's historic capital, famous for its planned streets, palaces, forts and distinctive pink architecture."
    },


    {
        name:"Varanasi",
        state:"Uttar Pradesh",
        category:"culture",

        wiki:"Varanasi",
        imageWiki:"Dashashwamedh Ghat",

        lat:25.3176,
        lng:82.9739,

        description:
        "Varanasi is one of India's oldest continuously inhabited cities, known for its ghats, temples, traditions and connection with the Ganges."
    },


    {
        name:"Munnar",
        state:"Kerala",
        category:"nature",

        wiki:"Munnar",
        imageWiki:"Munnar",

        lat:10.0889,
        lng:77.0595,

        description:
        "Munnar is a mountain destination in Kerala surrounded by tea plantations, forests, valleys and cool highland landscapes."
    },


    {
        name:"Leh",
        state:"Ladakh",
        category:"mountains",

        wiki:"Leh",
        imageWiki:"Leh Palace",

        lat:34.1526,
        lng:77.5771,

        description:
        "Leh is a high-altitude Himalayan town surrounded by dramatic mountains, monasteries and historic Ladakhi architecture."
    },


    {
        name:"Goa",
        state:"Goa",
        category:"culture",

        wiki:"Goa",
        imageWiki:"Basilica of Bom Jesus",

        lat:15.2993,
        lng:74.1240,

        description:
        "Goa combines coastal landscapes with Portuguese-era architecture, historic churches, villages and a distinctive cultural heritage."
    },


    {
        name:"Tawang",
        state:"Arunachal Pradesh",
        category:"mountains",

        wiki:"Tawang",
        imageWiki:"Tawang Monastery",

        lat:27.5860,
        lng:91.8590,

        description:
        "Tawang is a Himalayan destination known for high mountain landscapes, Buddhist heritage and Tawang Monastery."
    },


    {
        name:"Agra",
        state:"Uttar Pradesh",
        category:"heritage",

        wiki:"Agra",
        imageWiki:"Taj Mahal",

        lat:27.1767,
        lng:78.0081,

        description:
        "Agra is a historic city on the Yamuna known for the Taj Mahal, Agra Fort and its Mughal architectural heritage."
    },


    {
        name:"Jaisalmer",
        state:"Rajasthan",
        category:"heritage",

        wiki:"Jaisalmer",
        imageWiki:"Jaisalmer Fort",

        lat:26.9157,
        lng:70.9083,

        description:
        "Jaisalmer rises from the Thar Desert with its golden sandstone fort, havelis and historic desert architecture."
    },


    {
        name:"Darjeeling",
        state:"West Bengal",
        category:"mountains",

        wiki:"Darjeeling",
        imageWiki:"Darjeeling Himalayan Railway",

        lat:27.0410,
        lng:88.2663,

        description:
        "Darjeeling is a Himalayan hill town famous for tea gardens, mountain views and the historic Darjeeling Himalayan Railway."
    },


    {
        name:"Rishikesh",
        state:"Uttarakhand",
        category:"nature",

        wiki:"Rishikesh",
        imageWiki:"Lakshman Jhula",

        lat:30.0869,
        lng:78.2676,

        description:
        "Rishikesh lies along the Ganges at the Himalayan foothills and is known for its river landscape, ashrams and bridges."
    },


    {
        name:"Shillong",
        state:"Meghalaya",
        category:"nature",

        wiki:"Shillong",
        imageWiki:"Shillong",

        lat:25.5788,
        lng:91.8933,

        description:
        "Shillong is a green hill city surrounded by waterfalls, forests, valleys and the distinctive landscapes of Meghalaya."
    },


    {
        name:"Kochi",
        state:"Kerala",
        category:"culture",

        wiki:"Kochi",
        imageWiki:"Chinese fishing nets",

        lat:9.9312,
        lng:76.2673,

        description:
        "Kochi is a historic coastal city shaped by centuries of maritime trade and a mixture of Indian, Arab, Chinese and European influences."
    },


    {
        name:"Jodhpur",
        state:"Rajasthan",
        category:"heritage",

        wiki:"Jodhpur",
        imageWiki:"Mehrangarh",

        lat:26.2389,
        lng:73.0243,

        description:
        "Jodhpur is the Blue City of Rajasthan, dominated by the massive Mehrangarh Fort and surrounded by historic neighbourhoods."
    }

];


/* =========================================================
   GLOBAL VARIABLES
========================================================= */

let map = null;
let marker = null;


/* =========================================================
   WELCOME BUTTON
========================================================= */

function enterWebsite(){

    const intro =
        document.getElementById("intro");

    if(!intro){
        return;
    }

    intro.style.opacity = "0";
    intro.style.transform = "scale(1.03)";
    intro.style.pointerEvents = "none";

    setTimeout(function(){

        intro.style.display = "none";

        document.body.style.overflowX = "hidden";
        document.body.style.overflowY = "auto";

        if(map){

            setTimeout(function(){

                map.invalidateSize();

            },250);

        }

    },900);
}


/*
 Extra mobile-safe event listener.
*/

document.addEventListener(
    "DOMContentLoaded",
    function(){

        const button =
            document.getElementById(
                "enterButton"
            );

        if(button){

            button.addEventListener(
                "click",
                enterWebsite
            );

            button.addEventListener(
                "touchend",
                function(event){

                    event.preventDefault();

                    enterWebsite();

                },
                {
                    passive:false
                }
            );

        }

    }
);


/* =========================================================
   WIKIPEDIA API
========================================================= */

const WIKI_API =
    "https://en.wikipedia.org/w/api.php";


/* =========================================================
   GET WIKIPEDIA PAGE
========================================================= */

async function getWikipediaPage(title){

    const params = new URLSearchParams({

        action:"query",

        format:"json",

        origin:"*",

        redirects:"1",

        prop:
            "pageimages|coordinates|extracts|info",

        inprop:"url",

        exintro:"1",

        explaintext:"1",

        piprop:
            "thumbnail|original|name",

        pithumbsize:"1400",

        titles:title

    });


    const response =
        await fetch(
            WIKI_API + "?" + params.toString()
        );


    if(!response.ok){

        throw new Error(
            "Wikipedia request failed"
        );

    }


    const data =
        await response.json();


    if(
        !data.query ||
        !data.query.pages
    ){

        return null;

    }


    const page =
        Object.values(
            data.query.pages
        )[0];


    if(!page || page.missing){

        return null;

    }


    return page;

}


/* =========================================================
   CORRECT IMAGE SYSTEM
========================================================= */

/*
 IMPORTANT:

 1. Try the specific landmark article.
 2. Try the destination article.
 3. If both fail, use a neutral visual.
 4. NEVER use Taj Mahal as a generic fallback.
*/

async function getCorrectImage(place){

    try{

        const landmarkPage =
            await getWikipediaPage(
                place.imageWiki
            );


        if(
            landmarkPage &&
            landmarkPage.original &&
            landmarkPage.original.source
        ){

            return landmarkPage.original.source;

        }


        if(
            landmarkPage &&
            landmarkPage.thumbnail &&
            landmarkPage.thumbnail.source
        ){

            return landmarkPage.thumbnail.source;

        }

    }
    catch(error){

        console.warn(
            "Landmark image unavailable:",
            place.name,
            error
        );

    }


    try{

        const cityPage =
            await getWikipediaPage(
                place.wiki
            );


        if(
            cityPage &&
            cityPage.original &&
            cityPage.original.source
        ){

            return cityPage.original.source;

        }


        if(
            cityPage &&
            cityPage.thumbnail &&
            cityPage.thumbnail.source
        ){

            return cityPage.thumbnail.source;

        }

    }
    catch(error){

        console.warn(
            "Destination image unavailable:",
            place.name,
            error
        );

    }


    return null;
}


/* =========================================================
   IMAGE ERROR
========================================================= */

function imageError(img){

    img.onerror = null;

    img.removeAttribute("src");

    img.classList.add(
        "image-fallback"
    );

}


/* =========================================================
   CREATE DESTINATION CARD
========================================================= */

async function createCard(
    place,
    index
){

    const card =
        document.createElement(
            "article"
        );

    card.className =
        "destination-card";


    card.innerHTML = `

        <img
            class="destination-image"
            alt="${escapeHTML(place.name)}"
        >

        <div class="destination-overlay">

            <div class="destination-number">
                ${String(index + 1).padStart(2,"0")}
            </div>

            <div class="destination-name">
                ${escapeHTML(place.name)}
            </div>

            <div class="destination-state">
                ${escapeHTML(place.state)}
            </div>

        </div>

        <div class="destination-arrow">
            ↗
        </div>

    `;


    card.addEventListener(
        "click",
        function(){

            openDestination(place);

        }
    );


    const img =
        card.querySelector(
            ".destination-image"
        );


    img.addEventListener(
        "error",
        function(){

            imageError(img);

        }
    );


    const image =
        await getCorrectImage(place);


    if(image){

        img.src = image;

    }
    else{

        img.classList.add(
            "image-fallback"
        );

    }


    return card;
}


/* =========================================================
   RENDER DESTINATIONS
========================================================= */

async function renderDestinations(
    filter="all"
){

    const grid =
        document.getElementById(
            "destinationGrid"
        );


    grid.innerHTML =
        `<div class="loading">
            LOADING DESTINATIONS...
        </div>`;


    const filtered =
        places.filter(
            function(place){

                return (
                    filter === "all" ||
                    place.category === filter
                );

            }
        );


    grid.innerHTML = "";


    /*
     Load cards one by one.
     This prevents one failed Wikipedia
     request from stopping the whole website.
    */

    for(
        let i=0;
        i<filtered.length;
        i++
    ){

        try{

            const card =
                await createCard(
                    filtered[i],
                    i
                );

            grid.appendChild(card);

        }
        catch(error){

            console.error(
                "Card error:",
                filtered[i].name,
                error
            );

        }

    }

}


/* =========================================================
   FILTERS
========================================================= */

document.addEventListener(
    "DOMContentLoaded",
    function(){

        document
        .querySelectorAll(".filter")
        .forEach(function(button){

            button.addEventListener(
                "click",
                async function(){

                    document
                    .querySelectorAll(".filter")
                    .forEach(function(btn){

                        btn.classList.remove(
                            "active"
                        );

                    });


                    button.classList.add(
                        "active"
                    );


                    await renderDestinations(
                        button.dataset.filter
                    );

                }
            );

        });

    }
);


/* =========================================================
   OPEN DESTINATION
========================================================= */

async function openDestination(place){

    const detail =
        document.getElementById(
            "detailSection"
        );


    detail.style.display =
        "block";


    detail.scrollIntoView({
        behavior:"smooth",
        block:"start"
    });


    document.getElementById(
        "detailKicker"
    ).textContent =
        place.state.toUpperCase();


    document.getElementById(
        "detailTitle"
    ).textContent =
        place.name;


    document.getElementById(
        "detailLocation"
    ).textContent =
        `${place.name}, ${place.state}, India`;


    document.getElementById(
        "detailText"
    ).textContent =
        place.description;


    const detailImage =
        document.getElementById(
            "detailImage"
        );


    detailImage.removeAttribute(
        "src"
    );


    detailImage.classList.remove(
        "image-fallback"
    );


    detailImage.onerror =
        function(){

            imageError(detailImage);

        };


    const image =
        await getCorrectImage(place);


    if(image){

        detailImage.src =
            image;

    }
    else{

        detailImage.classList.add(
            "image-fallback"
        );

    }


    const wikiButton =
        document.getElementById(
            "wikiButton"
        );


    wikiButton.href =
        "https://en.wikipedia.org/wiki/" +
        encodeURIComponent(
            place.wiki.replaceAll(
                " ",
                "_"
            )
        );


    await loadWikipedia(
        place
    );


    updateMap(
        place.lat,
        place.lng,
        place.name
    );

}


/* =========================================================
   WIKIPEDIA DETAILS
========================================================= */

async function loadWikipedia(place){

    const extract =
        document.getElementById(
            "wikiExtract"
        );


    extract.textContent =
        "Loading Wikipedia information...";


    try{

        const page =
            await getWikipediaPage(
                place.wiki
            );


        if(!page){

            extract.textContent =
                "Wikipedia information could not be found.";

            return;

        }


        if(page.extract){

            extract.textContent =
                page.extract;

        }
        else{

            extract.textContent =
                "No short Wikipedia introduction is available.";

        }


        /*
         If Wikipedia has coordinates,
         use them for the map.
        */

        if(
            page.coordinates &&
            page.coordinates[0]
        ){

            updateMap(
                page.coordinates[0].lat,
                page.coordinates[0].lon,
                place.name
            );

        }

    }
    catch(error){

        console.error(
            "Wikipedia details error:",
            error
        );


        extract.textContent =
            "Wikipedia is temporarily unavailable. You can still open the article using the button above.";

    }

}


/* =========================================================
   SEARCH
========================================================= */

let searchTimer = null;


document.addEventListener(
    "DOMContentLoaded",
    function(){

        const searchInput =
            document.getElementById(
                "searchInput"
            );


        searchInput.addEventListener(
            "input",
            function(){

                clearTimeout(
                    searchTimer
                );


                const query =
                    this.value.trim();


                if(query.length < 2){

                    document.getElementById(
                        "wikiResults"
                    ).innerHTML = "";

                    return;

                }


                searchTimer =
                    setTimeout(
                        function(){

                            searchWikipedia(
                                query
                            );

                        },
                        400
                    );

            }
        );

    }
);


/* =========================================================
   WIKIPEDIA SEARCH
========================================================= */

async function searchWikipedia(query){

    const results =
        document.getElementById(
            "wikiResults"
        );


    results.innerHTML =
        `<div class="loading">
            SEARCHING WIKIPEDIA...
        </div>`;


    try{

        const params =
            new URLSearchParams({

                action:"query",

                format:"json",

                origin:"*",

                generator:"search",

                gsrsearch:query,

                gsrnamespace:"0",

                gsrlimit:"7",

                prop:
                    "pageimages|extracts|info",

                inprop:"url",

                exintro:"1",

                explaintext:"1",

                piprop:"thumbnail",

                pithumbsize:"500"

            });


        const response =
            await fetch(
                WIKI_API +
                "?" +
                params.toString()
            );


        if(!response.ok){

            throw new Error(
                "Search failed"
            );

        }


        const data =
            await response.json();


        results.innerHTML = "";


        if(
            !data.query ||
            !data.query.pages
        ){

            results.innerHTML =
                `<div class="loading">
                    NO WIKIPEDIA RESULTS FOUND.
                </div>`;

            return;

        }


        const pages =
            Object.values(
                data.query.pages
            );


        pages.forEach(
            function(page){

                const item =
                    document.createElement(
                        "div"
                    );


                item.className =
                    "wiki-result";


                const image =
                    page.thumbnail &&
                    page.thumbnail.source
                    ?
                    `<img
                        src="${page.thumbnail.source}"
                        alt=""
                    >`
                    :
                    `<div
                        style="
                            width:100px;
                            min-width:100px;
                            height:75px;
                            background:#171717;
                        "
                    ></div>`;


                item.innerHTML = `

                    ${image}

                    <div>

                        <h3>
                            ${escapeHTML(page.title)}
                        </h3>

                        <p>
                            ${escapeHTML(
                                page.extract ||
                                "Explore this Wikipedia article."
                            ).slice(0,220)}
                        </p>

                    </div>

                `;


                item.addEventListener(
                    "click",
                    function(){

                        const matching =
                            places.find(
                                function(place){

                                    return (
                                        place.wiki
                                            .toLowerCase() ===
                                        page.title
                                            .toLowerCase()
                                    );

                                }
                            );


                        if(matching){

                            openDestination(
                                matching
                            );

                        }
                        else{

                            openSearchResult(
                                page
                            );

                        }

                    }
                );


                results.appendChild(
                    item
                );

            }
        );

    }
    catch(error){

        console.error(
            "Wikipedia search error:",
            error
        );


        results.innerHTML =
            `<div class="loading">
                WIKIPEDIA SEARCH IS TEMPORARILY UNAVAILABLE.
            </div>`;

    }

}


/* =========================================================
   OPEN SEARCH RESULT
========================================================= */

function openSearchResult(page){

    const detail =
        document.getElementById(
            "detailSection"
        );


    detail.style.display =
        "block";


    detail.scrollIntoView({
        behavior:"smooth",
        block:"start"
    });


    document.getElementById(
        "detailKicker"
    ).textContent =
        "WIKIPEDIA DISCOVERY";


    document.getElementById(
        "detailTitle"
    ).textContent =
        page.title;


    document.getElementById(
        "detailLocation"
    ).textContent =
        "Wikipedia discovery";


    document.getElementById(
        "detailText"
    ).textContent =
        page.extract ||
        "Explore this place through Wikipedia.";


    const image =
        document.getElementById(
            "detailImage"
        );


    image.classList.remove(
        "image-fallback"
    );


    image.removeAttribute(
        "src"
    );


    if(
        page.thumbnail &&
        page.thumbnail.source
    ){

        image.src =
            page.thumbnail.source;

    }
    else{

        image.classList.add(
            "image-fallback"
        );

    }


    image.onerror =
        function(){

            imageError(image);

        };


    document.getElementById(
        "wikiButton"
    ).href =
        "https://en.wikipedia.org/wiki/" +
        encodeURIComponent(
            page.title.replaceAll(
                " ",
                "_"
            )
        );


    document.getElementById(
        "wikiExtract"
    ).textContent =
        page.extract ||
        "No introduction available.";

}


/* =========================================================
   MAP
========================================================= */

function initializeMap(){

    map =
        L.map(
            "map"
        ).setView(
            [22.9734,78.6569],
            5
        );


    L.tileLayer(
        "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
        {
            maxZoom:19,

            attribution:
                "&copy; OpenStreetMap contributors"
        }
    ).addTo(map);

}


/* =========================================================
   UPDATE MAP
========================================================= */

function updateMap(
    lat,
    lng,
    title
){

    if(!map){

        return;

    }


    map.setView(
        [lat,lng],
        13,
        {
            animate:true
        }
    );


    if(marker){

        map.removeLayer(
            marker
        );

    }


    marker =
        L.marker(
            [lat,lng]
        )
        .addTo(map)
        .bindPopup(
            `<strong>
                ${escapeHTML(title)}
            </strong>`
        )
        .openPopup();


    setTimeout(
        function(){

            map.invalidateSize();

        },
        250
    );

}


/* =========================================================
   GALLERY
========================================================= */

async function renderGallery(){

    const gallery =
        document.getElementById(
            "galleryGrid"
        );


    gallery.innerHTML = "";


    const galleryPlaces =
        places.slice(0,8);


    for(
        const place of galleryPlaces
    ){

        try{

            const image =
                await getCorrectImage(
                    place
                );


            const img =
                document.createElement(
                    "img"
                );


            img.alt =
                `${place.name}, ${place.state}`;


            img.onerror =
                function(){

                    imageError(img);

                };


            if(image){

                img.src =
                    image;

            }
            else{

                img.classList.add(
                    "image-fallback"
                );

            }


            gallery.appendChild(
                img
            );

        }
        catch(error){

            console.error(
                "Gallery image error:",
                place.name,
                error
            );

        }

    }

}


/* =========================================================
   ESCAPE HTML
========================================================= */

function escapeHTML(value){

    return String(value)
        .replaceAll(
            "&",
            "&amp;"
        )
        .replaceAll(
            "<",
            "&lt;"
        )
        .replaceAll(
            ">",
            "&gt;"
        )
        .replaceAll(
            '"',
            "&quot;"
        )
        .replaceAll(
            "'",
            "&#039;"
        );

}


/* =========================================================
   START WEBSITE
========================================================= */

document.addEventListener(
    "DOMContentLoaded",
    async function(){

        /*
         IMPORTANT:
         These are isolated so if Wikipedia
         has a temporary problem, the rest
         of the website still loads.
        */

        try{

            initializeMap();

        }
        catch(error){

            console.error(
                "Map initialization failed:",
                error
            );

        }


        try{

            await renderDestinations();

        }
        catch(error){

            console.error(
                "Destination loading failed:",
                error
            );

        }


        try{

            await renderGallery();

        }
        catch(error){

            console.error(
                "Gallery loading failed:",
                error
            );

        }

    }
);

</script>

</body>
</html>

