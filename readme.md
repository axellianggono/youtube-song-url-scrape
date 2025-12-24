# Scrape Youtube Songs
Dapatkan daftar url youtube lagu yang diinginkan.

## Cara penggunaan
1. Masuk ke dev tool youtube
2. Copas code ini (edit bagian songs)
```js
const songs = [
  "Touch",
  "Open Letter",
  "Only You",
]; // isi sesuai daftar lagu yang diinginkan

async function getVideoLink(query) {
  const res = await fetch(
    "https://www.youtube.com/results?search_query=" +
      encodeURIComponent(query)
  );
  const text = await res.text();

  const match = text.match(/"videoId":"(.*?)"/);
  if (!match) return null;

  return `https://www.youtube.com/watch?v=${match[1]}&list=RD${match[1]}&start_radio=1`;
}

(async () => {
  const results = [];

  for (const song of songs) {
    console.log("Mencari:", song);
    const url = await getVideoLink(song);
    if (url) {
      console.log(url);
      results.push(url);
    } else {
      console.log("Tidak ditemukan:", song);
    }

    await new Promise(r => setTimeout(r, 1500));
  }

  console.log("\n=== HASIL AKHIR ===");
  console.log(results.join("\n"));
})();
```