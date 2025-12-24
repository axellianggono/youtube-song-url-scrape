1. Kunjungi playlist spotify di web
2. Buka devtools lalu paste

```js

const songs = new Set();

const observer = new MutationObserver(() => {
  document.querySelectorAll(
    'div[data-encore-id="text"].standalone-ellipsis-one-line'
  ).forEach(el => {
    const text = el.textContent.trim();
    if (text) songs.add(text);
  });

  console.clear();
  console.log(`Total lagu tertangkap: ${songs.size}`);
});

observer.observe(document.body, {
  childList: true,
  subtree: true
});

const scrollInterval = setInterval(() => {
  window.scrollBy(0, 800);
}, 800);

// Hentikan setelah 30 detik
setTimeout(() => {
  clearInterval(scrollInterval);
  observer.disconnect();
  console.log("SELESAI");
  console.log([...songs]);
}, 30000);
```