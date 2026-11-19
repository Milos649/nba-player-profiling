# 🏀 NBA Player Statistical Profiling, Era Evolution & Recommender System

Többváltozós adattudományi elemzés az NBA játékosok szezonstatisztikáin: funkcionális játékosprofilok feltárása, a modern *Pace-and-Space* korszakváltás idősoros vizsgálata és tartalomalapú játékos-ajánlórendszer.

## Főbb vizsgálatok és módszertan

1. **Adattisztítás és túlélési torzítás (Survivorship Bias):**
   - A szezon közben csapatot váltó játékosok (`2TM`/`3TM`) deduplikálása a teljes szezonos sorok megtartásával (2022–2026).
   - A 36 percre vetített mutatók kis mintás zajának kiszűrése ($\ge 20$ mérkőzés, $\ge 500$ pályán töltött perc), valamint a szűrés által okozott túlélési torzítás kvantitatív vizsgálata (`TS%`, `BPM`).
2. **Magas dimenziós reprezentáció és 2D térképek (PCA vs. t-SNE):**
   - 14 darab, játékidőre normált (`Per 36 Minutes`) és fejlett (`Advanced`) mutató transzformációja (`log1p` + `RobustScaler`).
   - Globális (PCA) és lokális (t-SNE) dimenziócsökkentés összevetése, valamint a $k=15$ szomszédság-tisztaság (*Neighborhood Purity*) mérése az 5 hivatalos posztra (`PG, SG, SF, PF, C`).
3. **Játékosprofilok és Poszt-anomáliák (K-Means & DBSCAN):**
   - $k$-diagnosztika (Inertia, Silhouette, minimális klaszterméret) alapján 5 funkcionális szerepkör azonosítása és szegmenskártyás profilozása.
   - Egyedi szupersztár- és specialista-outlierek detektálása sűrűségalapú DBSCAN algoritmussal.
   - Posztjuktól eltérő játékstílusú játékosok (*Point Centerek*, *Stretch 5* centerek, lepattanózó hátvédek) azonosítása.
4. **Az NBA játékstílusának evolúciója (1980–2026):**
   - 47 szezon dobáskiválasztási trendjeinek idősoros vizsgálata, posztonkénti idősor-hőtérkép és a szezonok közötti *Cosine Similarity* mátrix a korszakhatárok kimutatására.
5. **Tartalomalapú játékos-ajánlórendszer (Content-Based Filtering):**
   - Top-5 hasonló játékos keresése koszinusz-hasonlóság alapján, az önmagára találás és több-szezonos duplikációk kiszűrésével.
   - A nyers meccsátlagok arány-csapdájának és a központosított, skálázott 14D stílusvektor előnyeinek összevetése `Precision@5` metrikával (`79,1%` vs. `47,4%`).

## Technológiák
- **Python**, **Pandas**, **NumPy**
- **Scikit-learn** (`PCA`, `TSNE`, `KMeans`, `DBSCAN`, `RobustScaler`, `NearestNeighbors`, `cosine_similarity`)
- **Matplotlib**, **Seaborn**

## Adatforrás
- Kaggle: [NBA Stats (1947-present)](https://www.kaggle.com/datasets/sumitrodatta/nba-aba-baa-stats)