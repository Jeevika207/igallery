# Ex.08 Design of Interactive Image Gallery
## Date: 12/05/2025

## AIM:
To design a web application for an inteactive image gallery with minimum five images.

## DESIGN STEPS:

### Step 1:
Clone the github repository and create Django admin interface.

### Step 2:
Change settings.py file to allow request from all hosts.

### Step 3:
Use CSS for positioning and styling.

### Step 4:
Write JavaScript program for implementing interactivity.

### Step 5:
Validate the HTML and CSS code.

### Step 6:
Publish the website in the given URL.

## PROGRAM :
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive Photo Gallery</title>
  <style>
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: linear-gradient(135deg, #a8e063 0%, #56ab2f 100%);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }
    header {
      background: #333;
      color: #fff;
      text-align: center;
      padding: 2rem 1rem 1rem 1rem;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }
    header h1 {
      margin: 0;
      font-size: 2.2rem;
      letter-spacing: 2px;
    }
    .search-bar {
      display: flex;
      justify-content: center;
      margin: 2rem 0 1rem 0;
    }
    #search {
      width: 300px;
      padding: 0.7rem 1rem;
      border: 1px solid #ccc;
      border-radius: 30px;
      font-size: 1rem;
      outline: none;
      transition: border 0.2s;
    }
    #search:focus {
      border: 1.5px solid #56ab2f;
    }
    main {
      flex: 1;
      padding: 1rem 5vw 2rem 5vw;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .gallery {
      width: 100%;
      max-width: 1100px;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 1.5rem;
    }
    .photo-item {
      position: relative;
      overflow: hidden;
      border-radius: 12px;
      box-shadow: 0 6px 18px rgba(0,0,0,0.13);
      background: #fff;
      transition: transform 0.2s;
    }
    .photo-item img {
      width: 100%;
      height: 180px;
      object-fit: cover;
      display: block;
      cursor: pointer;
      transition: transform 0.35s cubic-bezier(.19,1,.22,1);
    }
    .photo-item:hover img {
      transform: scale(1.07);
    }
    .photo-title {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      background: rgba(44,62,80,0.65);
      color: #fff;
      text-align: center;
      padding: 0.6rem 0;
      font-size: 1.1rem;
      letter-spacing: 1px;
      opacity: 0.95;
    }
    .lightbox {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100vw; height: 100vh;
      background: rgba(0,0,0,0.88);
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }
    .lightbox img {
      max-width: 90vw;
      max-height: 85vh;
      border-radius: 10px;
      box-shadow: 0 8px 32px rgba(0,0,0,0.18);
      background: #fff;
    }
    .lightbox:active, .lightbox:focus {
      outline: none;
    }
    footer {
      text-align: center;
      padding: 1.2rem 0 1.2rem 0;
      background: #222;
      color: #fff;
      font-size: 1.1rem;
      letter-spacing: 1px;
      margin-top: auto;
    }
    @media (max-width: 600px) {
      .gallery {
        grid-template-columns: 1fr;
      }
      main {
        padding: 1rem;
      }
      #search {
        width: 90vw;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>INTERACTIVE IMAGE GALLERY</h1>
  </header>
  <div class="search-bar">
    <input type="text" id="search" placeholder="Search images by name..." onkeyup="filterImages()">
  </div>
  <main>
    <section class="gallery">
      <div class="photo-item" data-title="AMG">
        <img src="amg.jpg" alt="AMG">
        <div class="photo-title">AMG</div>
      </div>
      <div class="photo-item" data-title="BNW">
        <img src="bnw.jpg" alt="BNW">
        <div class="photo-title">BNW</div>
      </div>
      <div class="photo-item" data-title="MUSTANG">
        <img src="mustang.jpg" alt="MUSTANG">
        <div class="photo-title">MUSTANG</div>
      </div>
      <div class="photo-item" data-title="BUGATTI">
        <img src="bugatti.jpg" alt="BUGATTI">
        <div class="photo-title">BUGATTI</div>
      </div>
      <div class="photo-item" data-title="SKYLINE">
        <img src="skyline.jpg" alt="SKYLINE">
        <div class="photo-title">SKYLINE</div>
      </div>
      <div class="photo-item" data-title="SUPRA">
        <img src="supra.jpg" alt="SUPRA">
        <div class="photo-title">SUPRA</div>
      </div>
    </section>
  </main>
  <div id="lightbox" class="lightbox" tabindex="-1" onclick="closeLightbox()">
    <img id="lightbox-img" src="" alt="Large View">
  </div>
  <footer>
    Designed by Jeevika R
  </footer>
  <script>
    // Lightbox functionality
    const photoItems = document.querySelectorAll('.photo-item img');
    const lightbox = document.getElementById('lightbox');
    const lightboxImg = document.getElementById('lightbox-img');
    photoItems.forEach(img => {
      img.addEventListener('click', (e) => {
        e.stopPropagation();
        lightbox.style.display = 'flex';
        lightboxImg.src = img.src;
        lightbox.focus();
      });
    });
    function closeLightbox() {
      lightbox.style.display = 'none';
      lightboxImg.src = '';
    }
    // Close on ESC
    document.addEventListener('keydown', function(e) {
      if (e.key === "Escape") closeLightbox();
    });
    // Filter images
    function filterImages() {
      const query = document.getElementById('search').value.toLowerCase();
      const photoItems = document.querySelectorAll('.photo-item');
      photoItems.forEach(item => {
        const title = item.getAttribute('data-title').toLowerCase();
        if (title.includes(query)) {
          item.style.display = '';
        } else {
          item.style.display = 'none';
        }
      });
    }
  </script>
</body>
</html>
```
## OUTPUT:
![image](https://github.com/user-attachments/assets/dedc0ba9-8066-49f8-9b8b-5f911ba3c6fc)

## RESULT:
The program for designing an interactive image gallery using HTML, CSS and JavaScript is executed successfully.
