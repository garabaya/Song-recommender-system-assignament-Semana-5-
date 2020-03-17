# Song recommender system assignament (Semana 5)
Jupyter notebook corresponding to the assignament of the Unit: "Recommender Systems" in the Coursera "Machine Learning Foundations: A Case Study Approach" course.


```python
import turicreate
```


```python
song_data = turicreate.SFrame('song_data.sframe')
```


```python
len(song_data)
```




    1116609



## Counting unique users
Unique users who have listened to songs by various artists


```python
kanye_west_song_data = song_data[song_data['artist'] == 'Kanye West']
```


```python
len(kanye_west_song_data)
```




    3775




```python
kanye_west_users = kanye_west_song_data['user_id'].unique()
```


```python
len(kanye_west_users)
```




    2522




```python
len(song_data[song_data['artist'] == 'Foo Fighters']['user_id'].unique())
```




    2055




```python
len(song_data[song_data['artist'] == 'Taylor Swift']['user_id'].unique())
```




    3246




```python
len(song_data[song_data['artist'] == 'Lady GaGa']['user_id'].unique())
```




    2928



## Using groupby-aggregate to find the most popular and least popular artist


```python
artist_popularity = song_data.groupby(key_column_names='artist', operations={'total_count': turicreate.aggregate.SUM('listen_count')})
```


```python
artist_popularity.sort('total_count',ascending=False)
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">artist</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">total_count</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Kings Of Leon</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">43218</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Dwight Yoakam</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">40619</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Björk</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">38889</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Coldplay</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">35362</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Florence + The Machine</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">33387</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Justin Bieber</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">29715</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Alliance Ethnik</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">26689</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">OneRepublic</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">25754</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Train</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">25402</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">The Black Keys</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">22184</td>
    </tr>
</table>
[3375 rows x 2 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>




```python
artist_popularity.sort('total_count')
```




<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">artist</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">total_count</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">William Tabbert</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">14</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Reel Feelings</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">24</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Beyoncé feat. Bun B and<br>Slim Thug ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">26</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Diplo</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">30</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Boggle Karaoke</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">30</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">harvey summers</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">31</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Nâdiya</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">36</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Jody Bernal</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">38</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Aneta Langerova</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">38</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Kanye West / Talib Kweli<br>/ Q-Tip / Common / ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">38</td>
    </tr>
</table>
[3375 rows x 2 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>



## Using groupby-aggregate to find the most recommended songs


```python
train_data,test_data = song_data.random_split(.8,seed=0)
```


```python
personalized_model = turicreate.item_similarity_recommender.create(train_data,
                                                                  user_id = 'user_id',
                                                                  item_id = 'song')
```


<pre>Warning: Ignoring columns song_id, listen_count, title, artist;</pre>



<pre> To use one of these as a rating column, specify the column name to be used as target</pre>



<pre>    and use a method that allows the use of a target.</pre>



<pre>Preparing data set.</pre>



<pre>    Data has 893580 observations with 66085 users and 9952 items.</pre>



<pre>    Data prepared in: 1.52548s</pre>



<pre>Training model from provided data.</pre>



<pre>Gathering per-item and per-user statistics.</pre>



<pre>+--------------------------------+------------+</pre>



<pre>| Elapsed Time (Item Statistics) | % Complete |</pre>



<pre>+--------------------------------+------------+</pre>



<pre>| 6.229ms                        | 1.5        |</pre>



<pre>| 92.015ms                       | 100        |</pre>



<pre>+--------------------------------+------------+</pre>



<pre>Setting up lookup tables.</pre>



<pre>Processing data in one pass using dense lookup tables.</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>| Elapsed Time (Constructing Lookups) | Total % Complete | Items Processed |</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>| 30.42s                              | 4.75             | 478             |</pre>



<pre>| 33.27s                              | 100              | 9952            |</pre>



<pre>+-------------------------------------+------------------+-----------------+</pre>



<pre>Finalizing lookup tables.</pre>



<pre>Generating candidate set for working with new users.</pre>



<pre>Finished training in 35.574s</pre>


We are going to make recommendations for the users in the test data, but there are over 200,000 users (58,628 unique users) in the test set. Computing recommendations for these many users can be slow in some computers. Thus, we will use only the first 10,000 users only in this question


```python
subset_test_users = test_data['user_id'].unique()[0:10000]
```


```python
personalized_model.recommend(subset_test_users,k=1).groupby(key_column_names='song', operations={'count': turicreate.aggregate.COUNT()}).sort('count',ascending=False)
```


<pre>recommendations finished on 1000/10000 queries. users per second: 2979.09</pre>



<pre>recommendations finished on 2000/10000 queries. users per second: 2790.17</pre>



<pre>recommendations finished on 3000/10000 queries. users per second: 2808.5</pre>



<pre>recommendations finished on 4000/10000 queries. users per second: 2414.47</pre>



<pre>recommendations finished on 5000/10000 queries. users per second: 2166.21</pre>



<pre>recommendations finished on 6000/10000 queries. users per second: 2227.86</pre>



<pre>recommendations finished on 7000/10000 queries. users per second: 2303.45</pre>



<pre>recommendations finished on 8000/10000 queries. users per second: 2361.66</pre>



<pre>recommendations finished on 9000/10000 queries. users per second: 2394.69</pre>



<pre>recommendations finished on 10000/10000 queries. users per second: 2339.02</pre>





<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">song</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">count</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Undo - Björk</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">429</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Secrets - OneRepublic</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">399</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Revelry - Kings Of Leon</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">230</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">You&#x27;re The One - Dwight<br>Yoakam ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">155</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Hey_ Soul Sister - Train</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">113</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sehr kosmisch - Harmonia</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">113</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Fireflies - Charttraxx<br>Karaoke ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">102</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Horn Concerto No. 4 in E<br>flat K495: II. Romance ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">91</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">OMG - Usher featuring<br>will.i.am ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">70</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">The Scientist - Coldplay</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">50</td>
    </tr>
</table>
[3119 rows x 2 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>



### Let's try with entire data set (crossing fingers)


```python
test_users = test_data['user_id'].unique()
```


```python
personalized_model.recommend(test_users,k=1).groupby(key_column_names='song', operations={'count': turicreate.aggregate.COUNT()}).sort('count',ascending=False)
```


<pre>recommendations finished on 1000/58628 queries. users per second: 3205.22</pre>



<pre>recommendations finished on 2000/58628 queries. users per second: 3016.01</pre>



<pre>recommendations finished on 3000/58628 queries. users per second: 2953.83</pre>



<pre>recommendations finished on 4000/58628 queries. users per second: 2956.92</pre>



<pre>recommendations finished on 5000/58628 queries. users per second: 2930.78</pre>



<pre>recommendations finished on 6000/58628 queries. users per second: 2930.12</pre>



<pre>recommendations finished on 7000/58628 queries. users per second: 2862.09</pre>



<pre>recommendations finished on 8000/58628 queries. users per second: 2855.76</pre>



<pre>recommendations finished on 9000/58628 queries. users per second: 2863.88</pre>



<pre>recommendations finished on 10000/58628 queries. users per second: 2871.87</pre>



<pre>recommendations finished on 11000/58628 queries. users per second: 2871.5</pre>



<pre>recommendations finished on 12000/58628 queries. users per second: 2872.79</pre>



<pre>recommendations finished on 13000/58628 queries. users per second: 2876.84</pre>



<pre>recommendations finished on 14000/58628 queries. users per second: 2869.17</pre>



<pre>recommendations finished on 15000/58628 queries. users per second: 2871.8</pre>



<pre>recommendations finished on 16000/58628 queries. users per second: 2874.15</pre>



<pre>recommendations finished on 17000/58628 queries. users per second: 2875.69</pre>



<pre>recommendations finished on 18000/58628 queries. users per second: 2880.68</pre>



<pre>recommendations finished on 19000/58628 queries. users per second: 2884.07</pre>



<pre>recommendations finished on 20000/58628 queries. users per second: 2884.58</pre>



<pre>recommendations finished on 21000/58628 queries. users per second: 2897.36</pre>



<pre>recommendations finished on 22000/58628 queries. users per second: 2907.86</pre>



<pre>recommendations finished on 23000/58628 queries. users per second: 2904.69</pre>



<pre>recommendations finished on 24000/58628 queries. users per second: 2905.93</pre>



<pre>recommendations finished on 25000/58628 queries. users per second: 2908</pre>



<pre>recommendations finished on 26000/58628 queries. users per second: 2912.56</pre>



<pre>recommendations finished on 27000/58628 queries. users per second: 2910.71</pre>



<pre>recommendations finished on 28000/58628 queries. users per second: 2915.47</pre>



<pre>recommendations finished on 29000/58628 queries. users per second: 2917.55</pre>



<pre>recommendations finished on 30000/58628 queries. users per second: 2920.42</pre>



<pre>recommendations finished on 31000/58628 queries. users per second: 2923.92</pre>



<pre>recommendations finished on 32000/58628 queries. users per second: 2922.08</pre>



<pre>recommendations finished on 33000/58628 queries. users per second: 2919.61</pre>



<pre>recommendations finished on 34000/58628 queries. users per second: 2916.27</pre>



<pre>recommendations finished on 35000/58628 queries. users per second: 2916.27</pre>



<pre>recommendations finished on 36000/58628 queries. users per second: 2916.84</pre>



<pre>recommendations finished on 37000/58628 queries. users per second: 2920.34</pre>



<pre>recommendations finished on 38000/58628 queries. users per second: 2918.57</pre>



<pre>recommendations finished on 39000/58628 queries. users per second: 2918.2</pre>



<pre>recommendations finished on 40000/58628 queries. users per second: 2914.99</pre>



<pre>recommendations finished on 41000/58628 queries. users per second: 2917.25</pre>



<pre>recommendations finished on 42000/58628 queries. users per second: 2914.41</pre>



<pre>recommendations finished on 43000/58628 queries. users per second: 2913.49</pre>



<pre>recommendations finished on 44000/58628 queries. users per second: 2911.42</pre>



<pre>recommendations finished on 45000/58628 queries. users per second: 2912.11</pre>



<pre>recommendations finished on 46000/58628 queries. users per second: 2911.43</pre>



<pre>recommendations finished on 47000/58628 queries. users per second: 2912.05</pre>



<pre>recommendations finished on 48000/58628 queries. users per second: 2913.61</pre>



<pre>recommendations finished on 49000/58628 queries. users per second: 2912.26</pre>



<pre>recommendations finished on 50000/58628 queries. users per second: 2875.57</pre>



<pre>recommendations finished on 51000/58628 queries. users per second: 2872.38</pre>



<pre>recommendations finished on 52000/58628 queries. users per second: 2832.83</pre>



<pre>recommendations finished on 53000/58628 queries. users per second: 2831.71</pre>



<pre>recommendations finished on 54000/58628 queries. users per second: 2833.2</pre>



<pre>recommendations finished on 55000/58628 queries. users per second: 2831.75</pre>



<pre>recommendations finished on 56000/58628 queries. users per second: 2822.38</pre>



<pre>recommendations finished on 57000/58628 queries. users per second: 2826.48</pre>



<pre>recommendations finished on 58000/58628 queries. users per second: 2830.63</pre>





<div style="max-height:1000px;max-width:1500px;overflow:auto;"><table frame="box" rules="cols">
    <tr>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">song</th>
        <th style="padding-left: 1em; padding-right: 1em; text-align: center">count</th>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Undo - Björk</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2527</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Secrets - OneRepublic</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">2250</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Revelry - Kings Of Leon</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">1311</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">You&#x27;re The One - Dwight<br>Yoakam ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">965</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Sehr kosmisch - Harmonia</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">651</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Fireflies - Charttraxx<br>Karaoke ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">639</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Hey_ Soul Sister - Train</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">633</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">Horn Concerto No. 4 in E<br>flat K495: II. Romance ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">522</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">OMG - Usher featuring<br>will.i.am ...</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">394</td>
    </tr>
    <tr>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">The Scientist - Coldplay</td>
        <td style="padding-left: 1em; padding-right: 1em; text-align: center; vertical-align: top">265</td>
    </tr>
</table>
[5767 rows x 2 columns]<br/>Note: Only the head of the SFrame is printed.<br/>You can use print_rows(num_rows=m, num_columns=n) to print more rows and columns.
</div>




```python

```
