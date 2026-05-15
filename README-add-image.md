Umieść tutaj plik obrazu używany jako tło hero strony głównej.

Wymagane pliki (po wygenerowaniu zoptymalizowanych wersji):

- `/poradnia-hero-1920.webp` (szer. ~1920px)
- `/poradnia-hero-1280.webp` (szer. ~1280px)
- `/poradnia-hero-800.webp` (szer. ~800px)
- `/poradnia-hero-1920.jpg` (szer. ~1920px, fallback)
- `/poradnia-hero-1280.jpg` (szer. ~1280px, fallback)
- `/poradnia-hero-800.jpg` (szer. ~800px, fallback)

Zalecane źródło: oryginalny plik o rozdzielczości >= 1920×1080. Nazwij go tymczasowo `poradnia-hero-original.jpg` i umieść w katalogu `public/`.

Przykładowe polecenia do wygenerowania zoptymalizowanych plików (ImageMagick):

```bash
# WebP
magick poradnia-hero-original.jpg -resize 1920x -quality 75 -strip poradnia-hero-1920.webp
magick poradnia-hero-original.jpg -resize 1280x -quality 75 -strip poradnia-hero-1280.webp
magick poradnia-hero-original.jpg -resize 800x  -quality 75 -strip poradnia-hero-800.webp

# JPEG fallback
magick poradnia-hero-original.jpg -resize 1920x -quality 75 -strip poradnia-hero-1920.jpg
magick poradnia-hero-original.jpg -resize 1280x -quality 75 -strip poradnia-hero-1280.jpg
magick poradnia-hero-original.jpg -resize 800x  -quality 75 -strip poradnia-hero-800.jpg
```

Przykład z użyciem `sharp` (Node.js):

```js
const sharp = require("sharp");
const sizes = [1920, 1280, 800];
sizes.forEach(async (w) => {
  await sharp("public/poradnia-hero-original.jpg")
    .resize(w)
    .webp({ quality: 75 })
    .toFile(`public/poradnia-hero-${w}.webp`);
  await sharp("public/poradnia-hero-original.jpg")
    .resize(w)
    .jpeg({ quality: 75 })
    .toFile(`public/poradnia-hero-${w}.jpg`);
});
```

Po dodaniu wygenerowanych plików odśwież serwer dev (`npm run dev`) lub zbuduj stronę (`npm run build`). Strona główna używa teraz responsywnego `picture` i automatycznie wybierze najlepszy format i rozmiar.
