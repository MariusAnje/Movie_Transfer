# Movie_Transfer

## Files
1. Father --> Find overlapping movies
2. Cleansing --> data cleansing, find all attributes from IMDB title dataset for overlapping movies of IMDB vs Douban & IMDB vs MovieLens
3. HotAE --> Auto encoder test
4. title_DvI.txt --> overlapping movies of IMDB & Douban
5. title_MvI.txt --> overlapping movies of IMDB & MovieLens
6. Total_movie.tsv --> movie title and attributes for all overlapping movies, readable
7. \*_ID --> IDs for categorical attributes
8. ID_\* --> movie IDs pointing to attributes
9. np\* --> numpy file for attributes needed

## Important
1. **Key Index File:** ID_Title.tsv --> Movie titles and their ID in this repo
2. **Key data File:** npAttrEmbOv.npy --> a numpy file with K lines, each line: [0:3] numerical attributes, [3:159] one hot representation of categorical attributes, [159:209] text embeddings, [209] rating
3. **Key training File:** EmbInteresting.ipynb --> input: npAttrEmbOv.npy, model: MLP
4. **Key tricky File:** npIMDBvsDoubanSetOp.npy --> when loaded, you will get a *Dictionary* with 2 keys: "IMDBIntersectDouban" gives you the indexes of lines in file "npAttrEmbOv.npy" that are the intersection (IMDB $\cap$ Douban) and key "IMDBDifferenceDouban" gives you the difference (IMDB $-$ Douban). E.g.

```python
import numpy as np

total_dataset = np.load("npAttrEmbOv.npy")
IDs = np.load("npIMDBvsDoubanSetOp.npy")
IMDB_and_Douban = total_dataset[IDs["IMDBIntersectDouban"]]
IMDB_without_Douban = total_dataset[IDs["IMDBDifferenceDouban"]]
```

