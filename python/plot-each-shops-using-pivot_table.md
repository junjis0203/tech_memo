# 売り上げデータを店舗別にプロットする方法

店舗別に売り上げを集計する場合、[pivot_table](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.pivot_table.html)を使う。

店舗別に月別集計等をする場合は[groupby](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html)と[resample](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.resample.html)を使うが、その場合、以下のように変形していくと「店舗を横に並べた」DataFrameが作れる。

1. groupby
2. resample
3. sum
4. reset_index
5. pivot_table

具体的な方法は以下のnotebook参照。

<script src="https://gist.github.com/junjis0203/f4993fa80065918b2ac22d1fb12c479c.js"></script>
