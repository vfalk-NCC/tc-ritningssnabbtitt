# tc-ritningssnabbtitt
Trimble Connect Workspace-extension: ritningssnabbtitt med markup

## ⚡ Snabbvisning i 3D

Visar en PDF-ritning direkt i 3D-vyn, utan uppladdning eller konvertering.
Öppna ritningen och klicka **🧊 Lägg till i 3D-vy**, sedan **⚡ Visa
ritningen i 3D**.

- **Så fungerar det:** Trimble Connect kan inte visa en PDF eller bild i
  3D-vyn. En PDF utskriven från CAD består däremot av riktiga linjer.
  Appen tar ut linjerna och ritar dem med `markup.addLineMarkups`. De är
  vektorer och skarpa i alla zoomlägen.
- **Placering:** samma ankare, förskjutning, rotation, lutning och skala
  som resten av panelen. Med **Följ reglagen** ritas linjerna om när du
  drar i ett reglage. Sidans egen rotation (`/Rotate`) tas med.
- **Storlek:** kalibrerad storlek om ritningen är kalibrerad, annars
  pappersformatet × **Skala 1:N** (standard 1:100).
- **Detalj:** raka följdsegment slås ihop och dubbletter tas bort. Vid
  fler linjer än taket (Låg 5 000, Normal 15 000, Hög 40 000) visas de
  längsta.
- **Begränsningar:**
  - Kräver en vektor-PDF, inte skannad.
  - Linjerna blir enfärgade.
  - Fyllningar och riktig PDF-text följer inte med. Text som CAD ritat
    som linjer följer med.
  - Linjerna sparas inte och försvinner när 3D-vyn laddas om.

## Rättat: vektorutdragning med pdf.js 3.11

`extractPdfVectors` hittade noll linjer med den pdf.js-version appen
laddar (3.11.174), eftersom den bara läste det nyare pdf.js-formatet.
Den läser nu båda formaten och tar bara med vägar som faktiskt ritas
(stroke/fill), inte osynliga klippramar. Rättningen gäller även
DXF-exporten ("Vektorlinjer").
