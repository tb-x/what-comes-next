# What Comes Next?

A maker for printable picture-pattern sheets for young kids (around age 5). Each row is eight squares of pictures
that repeat or grow in their own way (circle, star, circle, star…), with some squares left grey. The child works
out the pattern and fills in the gaps. The sheets have no words, so they work for kids who can't read yet, and
they're made for a black-and-white printer. The answers are hidden in a QR code: scan it with a phone camera to
see the whole page solved.

Live at **https://tb-x.github.io/what-comes-next/**

## How it plays

- Print a sheet. Every row starts at the little black triangle on the left and reads to the right.
- Look at what repeats or changes, then draw the missing pictures in the grey squares, or cut out the pieces
  at the bottom of the page and glue them in. There's one piece for each grey square, the same size as a
  square, and they're mixed up so their order doesn't give the answer away.
- Scan the QR code at the top right. The answer page shows every row solved, with the squares that were grey
  shaded yellow.

The kinds of row:

- **Pictures**: a unit of pictures that repeats, like AB (○☆○☆), AAB, ABB, ABC, AABB, ABCD, ABCB…
- **White and black**: the same picture, outlined or filled in black, in a repeating pattern.
- **Big and small**: the same picture, big or small, in a repeating pattern.
- **Turning**: an arrow, a chomper or a square with one dark corner turns a quarter turn each time.
- **Counting**: a frame of 8 dots fills up one more each time (1 to 8), or empties one at a time.

A repeating row always shows its whole unit at least once without a gap, and the shortest repeat that fits the
squares that show also says exactly what goes in every gap, so each row has one answer.

## Levels

- **Easy**: pictures in AB, AAB or ABB, white/black AB and big/small AB. The last one or two squares are grey.
- **Medium**: three-picture and doubled patterns (ABC, AABB), turning, counting up. Two grey squares: the last
  one, and the one before it or one in the middle.
- **Hard**: four-picture patterns (ABCD, AABC, ABCB, ABAC, ABCC), turning both ways, counting up or down. Two or
  three grey squares anywhere after the first two.

## The maker page

- **Level**: Easy, Medium or Hard.
- **Pictures**: Shapes (circle, square, triangle, heart, star, diamond), Sun, fish, house… (sun, fish, house,
  tree, flower, moon), or A mix (each row picks one). Turning and counting rows use their own pictures.
- **Rows**: 4 to 8 rows on a page. With fewer rows they're spread out down the page.
- **Cut-out pieces**: yes or no.
- **Pages**: how many pages to print at once (up to 20).
- **New patterns** makes new rows for every page, ↻ on a page makes new ones for that page only, and **Print**
  prints them. The settings are remembered in this browser.
- Clicking the QR code on screen opens the answer page.

The QR code holds the whole page in the link: one part per row, separated by dots, each giving the kind of row,
the picture set, the base picture, then each square, a digit where it's shown and a letter (a = 0, b = 1 …)
where it's grey, e.g. `#ss0010101ab.cs012345ghi`. Nothing is stored anywhere, so a printed sheet keeps working
for as long as this page is online. The QR always points at the published page on GitHub Pages, even when the
maker runs on a local server.

## Running it

It's a single `index.html` with no build step. Serve the folder and open it:

```bash
python -m http.server 5218
```

Then go to http://localhost:5218/. Opening `index.html` straight from disk works too. The QR codes are made
by [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 1.4.4 (MIT), loaded from cdnjs.

After the first visit the page also works offline and can be added to a phone's Home Screen.

## Tuning knobs

Named constants at the top of the script in `index.html`:

| Constant | Default | What it does |
| --- | --- | --- |
| `DEFAULTS` | Easy, shapes, 6 rows, pieces, 1 page | Starting settings |
| `ROW` | 8 | Squares in a row |
| `ROWS` | 4 to 8 | The choices in the Rows list |
| `KINDS` | see Levels | Which kinds of row and patterns each level uses, and how often |
| `BLANKS` | Easy 1–2, Medium 2, Hard 2–3 | Grey squares in a row |
| `KIND_MAX` | 2 white/black, 2 big/small, 2 turning, 1 counting | Most rows of one kind on a page |
| `SHEETS_MAX` | 20 | Most pages printed at once |
| `MAX_CELL` | 22 mm | Biggest square on the sheet |
| `PIC` / `SMALL` | 0.74 / 0.55 | A picture's size in its square, and a small picture's size next to a big one |
| `ROW_GAP` / `ROW_GAP_MAX` | 0.45 / 1.1 squares | Gap between rows: at least, and at most when spreading them down the page |
| `QR` | 22 mm | Size of the answer QR code |
| `TRIES` | 60 | Attempts at a row with one clear answer before falling back to a plain AB row |
| `PUBLIC_URL` | `https://tb-x.github.io/what-comes-next/` | Where the QR code points |
