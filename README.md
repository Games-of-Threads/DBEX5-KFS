
# Database Exercise 5
>by Kristian Flejsborg Sørensen (cph-kf96)

I will exclude talking about data as chinook.x, given all assignments are releated to the chinook dataset.


```python
%load_ext sql
```


```python
%sql postgresql://appdev@data:5432/appdev
```




    'Connected: appdev@appdev'



## The union of all the tracks with genreid 18 and 20
the following command ask to select all things from the track where the genreid is the same as 20, then ask to combine all said data with a similair command with the difference being genreid as 18, thus effectively getting the union of all tracks with genreid 18 and 20, but in reverse order but it doesn't effect the result other than ordering.


```python
%sql (SELECT * FROM chinook.track WHERE genreid=20) UNION (SELECT * FROM chinook.track WHERE genreid=18);
```

    39 rows affected.





<table>
    <tr>
        <th>trackid</th>
        <th>name</th>
        <th>albumid</th>
        <th>mediatypeid</th>
        <th>genreid</th>
        <th>composer</th>
        <th>milliseconds</th>
        <th>bytes</th>
        <th>unitprice</th>
    </tr>
    <tr>
        <td>3248</td>
        <td>Take the Celestra</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2927677</td>
        <td>512381289</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3243</td>
        <td>Murder On the Rising Star</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2935894</td>
        <td>551759986</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3238</td>
        <td>The Living Legend, Pt. 2</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2923298</td>
        <td>515632754</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3230</td>
        <td>Lost Planet of the Gods, Pt. 2</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2914664</td>
        <td>534343985</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3249</td>
        <td>The Hand of God</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2924007</td>
        <td>536583079</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3226</td>
        <td>Battlestar Galactica, Pt. 1</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2952702</td>
        <td>541359437</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3242</td>
        <td>The Man With Nine Lives</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2956998</td>
        <td>577829804</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2837</td>
        <td>Crossroads, Pt. 1</td>
        <td>227</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2622622</td>
        <td>486233524</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2827</td>
        <td>Unfinished Business</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2622038</td>
        <td>528499160</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2836</td>
        <td>The Son Also Rises</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2621830</td>
        <td>499258498</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2831</td>
        <td>Taking a Break from All Your Worries</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2624207</td>
        <td>492700163</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3228</td>
        <td>Battlestar Galactica, Pt. 3</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2927802</td>
        <td>554509033</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3227</td>
        <td>Battlestar Galactica, Pt. 2</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2956081</td>
        <td>521387924</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3239</td>
        <td>Fire In Space</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2926593</td>
        <td>536784757</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2838</td>
        <td>Crossroads, Pt. 2</td>
        <td>227</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2869953</td>
        <td>497335706</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2834</td>
        <td>Dirty Hands</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2627961</td>
        <td>537648614</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2825</td>
        <td>A Measure of Salvation</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2563938</td>
        <td>489715554</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3244</td>
        <td>Greetings from Earth, Pt. 1</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2960293</td>
        <td>536824558</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3234</td>
        <td>The Gun On Ice Planet Zero, Pt. 2</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2924341</td>
        <td>546542281</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3241</td>
        <td>War of the Gods, Pt. 2</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2923381</td>
        <td>487899692</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3245</td>
        <td>Greetings from Earth, Pt. 2</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2903778</td>
        <td>527842860</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3235</td>
        <td>The Magnificent Warriors</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2924716</td>
        <td>570152232</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3231</td>
        <td>The Lost Warrior</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2920045</td>
        <td>558872190</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2833</td>
        <td>A Day In the Life</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2620245</td>
        <td>462818231</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3247</td>
        <td>Experiment In Terra</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2923548</td>
        <td>547982556</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3246</td>
        <td>Baltar&#x27;s Escape</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2922088</td>
        <td>525564224</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2829</td>
        <td>The Eye of Jupiter</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2618750</td>
        <td>517909587</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2828</td>
        <td>The Passage</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2623875</td>
        <td>490375760</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3233</td>
        <td>The Gun On Ice Planet Zero, Pt. 1</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2907615</td>
        <td>540980196</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3232</td>
        <td>The Long Patrol</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2925008</td>
        <td>513122217</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2819</td>
        <td>Battlestar Galactica: The Story So Far</td>
        <td>226</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2622250</td>
        <td>490750393</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2830</td>
        <td>Rapture</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2624541</td>
        <td>508406153</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3229</td>
        <td>Lost Planet of the Gods, Pt. 1</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2922547</td>
        <td>537812711</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2826</td>
        <td>Hero</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2713755</td>
        <td>506896959</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2835</td>
        <td>Maelstrom</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2622372</td>
        <td>514154275</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>2832</td>
        <td>The Woman King</td>
        <td>227</td>
        <td>3</td>
        <td>18</td>
        <td>None</td>
        <td>2626376</td>
        <td>552893447</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3236</td>
        <td>The Young Lords</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2863571</td>
        <td>587051735</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3240</td>
        <td>War of the Gods, Pt. 1</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2922630</td>
        <td>505761343</td>
        <td>1.99</td>
    </tr>
    <tr>
        <td>3237</td>
        <td>The Living Legend, Pt. 1</td>
        <td>253</td>
        <td>3</td>
        <td>20</td>
        <td>None</td>
        <td>2924507</td>
        <td>503641007</td>
        <td>1.99</td>
    </tr>
</table>



## The intersection of all the invoices that are cheaper than 10 dollars and the invoices that are more expensive than 5 dollars
the following command ask for all things from the invoice where the total cost is less than 10, however this would also get things below 5 dollars, so we ask it to get the intersection of said table with the command that selects all things from the invoice where the total cost is above 5 dollars, which gets the desired result of all invoices that is cheaper than 10 dollars and more expensive than 5 dollars.


```python
%sql (SELECT * from chinook.invoice where total < 10) INTERSECT (SELECT * from chinook.invoice where total > 5)
```

    115 rows affected.





<table>
    <tr>
        <th>invoiceid</th>
        <th>customerid</th>
        <th>invoicedate</th>
        <th>billingaddress</th>
        <th>billingcity</th>
        <th>billingstate</th>
        <th>billingcountry</th>
        <th>billingpostalcode</th>
        <th>total</th>
    </tr>
    <tr>
        <td>396</td>
        <td>18</td>
        <td>2013-10-08 00:00:00+00:00</td>
        <td>627 Broadway</td>
        <td>New York</td>
        <td>NY</td>
        <td>USA</td>
        <td>10012-2612</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>290</td>
        <td>32</td>
        <td>2012-06-27 00:00:00+00:00</td>
        <td>696 Osborne Street</td>
        <td>Winnipeg</td>
        <td>MB</td>
        <td>Canada</td>
        <td>R3L 2B9</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>185</td>
        <td>52</td>
        <td>2011-03-20 00:00:00+00:00</td>
        <td>202 Hoxton Street</td>
        <td>London</td>
        <td>None</td>
        <td>United Kingdom</td>
        <td>N1 5LH</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>53</td>
        <td>44</td>
        <td>2009-08-11 00:00:00+00:00</td>
        <td>Porthaninkatu 9</td>
        <td>Helsinki</td>
        <td>None</td>
        <td>Finland</td>
        <td>00530</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>10</td>
        <td>46</td>
        <td>2009-02-03 00:00:00+00:00</td>
        <td>3 Chatham Street</td>
        <td>Dublin</td>
        <td>Dublin</td>
        <td>Ireland</td>
        <td>None</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>172</td>
        <td>41</td>
        <td>2011-01-20 00:00:00+00:00</td>
        <td>11, Place Bellecour</td>
        <td>Lyon</td>
        <td>None</td>
        <td>France</td>
        <td>69002</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>52</td>
        <td>38</td>
        <td>2009-08-08 00:00:00+00:00</td>
        <td>Barbarossastraße 19</td>
        <td>Berlin</td>
        <td>None</td>
        <td>Germany</td>
        <td>10779</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>205</td>
        <td>44</td>
        <td>2011-06-20 00:00:00+00:00</td>
        <td>Porthaninkatu 9</td>
        <td>Helsinki</td>
        <td>None</td>
        <td>Finland</td>
        <td>00530</td>
        <td>7.96</td>
    </tr>
    <tr>
        <td>94</td>
        <td>30</td>
        <td>2010-02-10 00:00:00+00:00</td>
        <td>230 Elgin Street</td>
        <td>Ottawa</td>
        <td>ON</td>
        <td>Canada</td>
        <td>K2P 1L7</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>220</td>
        <td>6</td>
        <td>2011-08-22 00:00:00+00:00</td>
        <td>Rilská 3174/6</td>
        <td>Prague</td>
        <td>None</td>
        <td>Czech Republic</td>
        <td>14300</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>11</td>
        <td>52</td>
        <td>2009-02-06 00:00:00+00:00</td>
        <td>202 Hoxton Street</td>
        <td>London</td>
        <td>None</td>
        <td>United Kingdom</td>
        <td>N1 5LH</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>46</td>
        <td>6</td>
        <td>2009-07-11 00:00:00+00:00</td>
        <td>Rilská 3174/6</td>
        <td>Prague</td>
        <td>None</td>
        <td>Czech Republic</td>
        <td>14300</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>332</td>
        <td>24</td>
        <td>2012-12-30 00:00:00+00:00</td>
        <td>162 E Superior Street</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>USA</td>
        <td>60611</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>283</td>
        <td>53</td>
        <td>2012-05-27 00:00:00+00:00</td>
        <td>113 Lupus St</td>
        <td>London</td>
        <td>None</td>
        <td>United Kingdom</td>
        <td>SW1V 3EN</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>39</td>
        <td>27</td>
        <td>2009-06-10 00:00:00+00:00</td>
        <td>1033 N Park Ave</td>
        <td>Tucson</td>
        <td>AZ</td>
        <td>USA</td>
        <td>85719</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>318</td>
        <td>7</td>
        <td>2012-10-29 00:00:00+00:00</td>
        <td>Rotenturmstraße 4, 1010 Innere Stadt</td>
        <td>Vienne</td>
        <td>None</td>
        <td>Austria</td>
        <td>1010</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>347</td>
        <td>47</td>
        <td>2013-03-05 00:00:00+00:00</td>
        <td>Via Degli Scipioni, 43</td>
        <td>Rome</td>
        <td>RM</td>
        <td>Italy</td>
        <td>00192</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>213</td>
        <td>27</td>
        <td>2011-07-22 00:00:00+00:00</td>
        <td>1033 N Park Ave</td>
        <td>Tucson</td>
        <td>AZ</td>
        <td>USA</td>
        <td>85719</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>192</td>
        <td>31</td>
        <td>2011-04-20 00:00:00+00:00</td>
        <td>194A Chain Lake Drive</td>
        <td>Halifax</td>
        <td>NS</td>
        <td>Canada</td>
        <td>B3S 1C5</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>199</td>
        <td>10</td>
        <td>2011-05-21 00:00:00+00:00</td>
        <td>Rua Dr. Falcão Filho, 155</td>
        <td>São Paulo</td>
        <td>SP</td>
        <td>Brazil</td>
        <td>01007-010</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>367</td>
        <td>37</td>
        <td>2013-06-03 00:00:00+00:00</td>
        <td>Berger Straße 10</td>
        <td>Frankfurt</td>
        <td>None</td>
        <td>Germany</td>
        <td>60316</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>234</td>
        <td>23</td>
        <td>2011-10-23 00:00:00+00:00</td>
        <td>69 Salem Street</td>
        <td>Boston</td>
        <td>MA</td>
        <td>USA</td>
        <td>2113</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>24</td>
        <td>4</td>
        <td>2009-04-06 00:00:00+00:00</td>
        <td>Ullevålsveien 14</td>
        <td>Oslo</td>
        <td>None</td>
        <td>Norway</td>
        <td>0171</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>144</td>
        <td>7</td>
        <td>2010-09-18 00:00:00+00:00</td>
        <td>Rotenturmstraße 4, 1010 Innere Stadt</td>
        <td>Vienne</td>
        <td>None</td>
        <td>Austria</td>
        <td>1010</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>129</td>
        <td>43</td>
        <td>2010-07-15 00:00:00+00:00</td>
        <td>68, Rue Jouvence</td>
        <td>Dijon</td>
        <td>None</td>
        <td>France</td>
        <td>21000</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>143</td>
        <td>1</td>
        <td>2010-09-15 00:00:00+00:00</td>
        <td>Av. Brigadeiro Faria Lima, 2170</td>
        <td>São José dos Campos</td>
        <td>SP</td>
        <td>Brazil</td>
        <td>12227-000</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>346</td>
        <td>41</td>
        <td>2013-03-02 00:00:00+00:00</td>
        <td>11, Place Bellecour</td>
        <td>Lyon</td>
        <td>None</td>
        <td>France</td>
        <td>69002</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>74</td>
        <td>40</td>
        <td>2009-11-12 00:00:00+00:00</td>
        <td>8, Rue Hanovre</td>
        <td>Paris</td>
        <td>None</td>
        <td>France</td>
        <td>75002</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>109</td>
        <td>53</td>
        <td>2010-04-16 00:00:00+00:00</td>
        <td>113 Lupus St</td>
        <td>London</td>
        <td>None</td>
        <td>United Kingdom</td>
        <td>SW1V 3EN</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>66</td>
        <td>55</td>
        <td>2009-10-09 00:00:00+00:00</td>
        <td>421 Bourke Street</td>
        <td>Sidney</td>
        <td>NSW</td>
        <td>Australia</td>
        <td>2010</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>4</td>
        <td>14</td>
        <td>2009-01-06 00:00:00+00:00</td>
        <td>8210 111 ST NW</td>
        <td>Edmonton</td>
        <td>AB</td>
        <td>Canada</td>
        <td>T6G 2C7</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>171</td>
        <td>35</td>
        <td>2011-01-17 00:00:00+00:00</td>
        <td>Rua dos Campeões Europeus de Viena, 4350</td>
        <td>Porto</td>
        <td>None</td>
        <td>Portugal</td>
        <td>None</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>339</td>
        <td>3</td>
        <td>2013-01-30 00:00:00+00:00</td>
        <td>1498 rue Bélanger</td>
        <td>Montréal</td>
        <td>QC</td>
        <td>Canada</td>
        <td>H2G 1A7</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>389</td>
        <td>39</td>
        <td>2013-09-07 00:00:00+00:00</td>
        <td>4, Rue Milton</td>
        <td>Paris</td>
        <td>None</td>
        <td>France</td>
        <td>75009</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>276</td>
        <td>15</td>
        <td>2012-04-26 00:00:00+00:00</td>
        <td>700 W Pender Street</td>
        <td>Vancouver</td>
        <td>BC</td>
        <td>Canada</td>
        <td>V6C 1G8</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>270</td>
        <td>42</td>
        <td>2012-03-29 00:00:00+00:00</td>
        <td>9, Place Louis Barthou</td>
        <td>Bordeaux</td>
        <td>None</td>
        <td>France</td>
        <td>33000</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>262</td>
        <td>57</td>
        <td>2012-02-24 00:00:00+00:00</td>
        <td>Calle Lira, 198</td>
        <td>Santiago</td>
        <td>None</td>
        <td>Chile</td>
        <td>None</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>130</td>
        <td>49</td>
        <td>2010-07-18 00:00:00+00:00</td>
        <td>Ordynacka 10</td>
        <td>Warsaw</td>
        <td>None</td>
        <td>Poland</td>
        <td>00-358</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>25</td>
        <td>10</td>
        <td>2009-04-09 00:00:00+00:00</td>
        <td>Rua Dr. Falcão Filho, 155</td>
        <td>São Paulo</td>
        <td>SP</td>
        <td>Brazil</td>
        <td>01007-010</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>179</td>
        <td>20</td>
        <td>2011-02-20 00:00:00+00:00</td>
        <td>541 Del Medio Avenue</td>
        <td>Mountain View</td>
        <td>CA</td>
        <td>USA</td>
        <td>94040-111</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>269</td>
        <td>36</td>
        <td>2012-03-26 00:00:00+00:00</td>
        <td>Tauentzienstraße 8</td>
        <td>Berlin</td>
        <td>None</td>
        <td>Germany</td>
        <td>10789</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>354</td>
        <td>26</td>
        <td>2013-04-05 00:00:00+00:00</td>
        <td>2211 W Berry Street</td>
        <td>Fort Worth</td>
        <td>TX</td>
        <td>USA</td>
        <td>76110</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>409</td>
        <td>29</td>
        <td>2013-12-06 00:00:00+00:00</td>
        <td>796 Dundas Street West</td>
        <td>Toronto</td>
        <td>ON</td>
        <td>Canada</td>
        <td>M6J 1V1</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>158</td>
        <td>24</td>
        <td>2010-11-19 00:00:00+00:00</td>
        <td>162 E Superior Street</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>USA</td>
        <td>60611</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>284</td>
        <td>59</td>
        <td>2012-05-30 00:00:00+00:00</td>
        <td>3,Raj Bhavan Road</td>
        <td>Bangalore</td>
        <td>None</td>
        <td>India</td>
        <td>560001</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>235</td>
        <td>29</td>
        <td>2011-10-26 00:00:00+00:00</td>
        <td>796 Dundas Street West</td>
        <td>Toronto</td>
        <td>ON</td>
        <td>Canada</td>
        <td>M6J 1V1</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>59</td>
        <td>17</td>
        <td>2009-09-08 00:00:00+00:00</td>
        <td>1 Microsoft Way</td>
        <td>Redmond</td>
        <td>WA</td>
        <td>USA</td>
        <td>98052-8300</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>326</td>
        <td>51</td>
        <td>2012-12-02 00:00:00+00:00</td>
        <td>Celsiusg. 9</td>
        <td>Stockholm</td>
        <td>None</td>
        <td>Sweden</td>
        <td>11230</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>178</td>
        <td>14</td>
        <td>2011-02-17 00:00:00+00:00</td>
        <td>8210 111 ST NW</td>
        <td>Edmonton</td>
        <td>AB</td>
        <td>Canada</td>
        <td>T6G 2C7</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>304</td>
        <td>49</td>
        <td>2012-08-28 00:00:00+00:00</td>
        <td>Ordynacka 10</td>
        <td>Warsaw</td>
        <td>None</td>
        <td>Poland</td>
        <td>00-358</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>248</td>
        <td>40</td>
        <td>2011-12-24 00:00:00+00:00</td>
        <td>8, Rue Hanovre</td>
        <td>Paris</td>
        <td>None</td>
        <td>France</td>
        <td>75002</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>157</td>
        <td>18</td>
        <td>2010-11-16 00:00:00+00:00</td>
        <td>627 Broadway</td>
        <td>New York</td>
        <td>NY</td>
        <td>USA</td>
        <td>10012-2612</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>67</td>
        <td>2</td>
        <td>2009-10-12 00:00:00+00:00</td>
        <td>Theodor-Heuss-Straße 34</td>
        <td>Stuttgart</td>
        <td>None</td>
        <td>Germany</td>
        <td>70174</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>17</td>
        <td>25</td>
        <td>2009-03-06 00:00:00+00:00</td>
        <td>319 N. Frances Street</td>
        <td>Madison</td>
        <td>WI</td>
        <td>USA</td>
        <td>53703</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>102</td>
        <td>15</td>
        <td>2010-03-16 00:00:00+00:00</td>
        <td>700 W Pender Street</td>
        <td>Vancouver</td>
        <td>BC</td>
        <td>Canada</td>
        <td>V6C 1G8</td>
        <td>9.91</td>
    </tr>
    <tr>
        <td>116</td>
        <td>32</td>
        <td>2010-05-17 00:00:00+00:00</td>
        <td>696 Osborne Street</td>
        <td>Winnipeg</td>
        <td>MB</td>
        <td>Canada</td>
        <td>R3L 2B9</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>256</td>
        <td>25</td>
        <td>2012-01-27 00:00:00+00:00</td>
        <td>319 N. Frances Street</td>
        <td>Madison</td>
        <td>WI</td>
        <td>USA</td>
        <td>53703</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>374</td>
        <td>16</td>
        <td>2013-07-04 00:00:00+00:00</td>
        <td>1600 Amphitheatre Parkway</td>
        <td>Mountain View</td>
        <td>CA</td>
        <td>USA</td>
        <td>94043-1351</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>214</td>
        <td>33</td>
        <td>2011-07-25 00:00:00+00:00</td>
        <td>5112 48 Street</td>
        <td>Yellowknife</td>
        <td>NT</td>
        <td>Canada</td>
        <td>X1A 1N6</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>291</td>
        <td>38</td>
        <td>2012-06-30 00:00:00+00:00</td>
        <td>Barbarossastraße 19</td>
        <td>Berlin</td>
        <td>None</td>
        <td>Germany</td>
        <td>10779</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>375</td>
        <td>22</td>
        <td>2013-07-07 00:00:00+00:00</td>
        <td>120 S Orange Ave</td>
        <td>Orlando</td>
        <td>FL</td>
        <td>USA</td>
        <td>32801</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>81</td>
        <td>19</td>
        <td>2009-12-13 00:00:00+00:00</td>
        <td>1 Infinite Loop</td>
        <td>Cupertino</td>
        <td>CA</td>
        <td>USA</td>
        <td>95014</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>263</td>
        <td>4</td>
        <td>2012-02-27 00:00:00+00:00</td>
        <td>Ullevålsveien 14</td>
        <td>Oslo</td>
        <td>None</td>
        <td>Norway</td>
        <td>0171</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>353</td>
        <td>20</td>
        <td>2013-04-02 00:00:00+00:00</td>
        <td>541 Del Medio Avenue</td>
        <td>Mountain View</td>
        <td>CA</td>
        <td>USA</td>
        <td>94040-111</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>123</td>
        <td>11</td>
        <td>2010-06-17 00:00:00+00:00</td>
        <td>Av. Paulista, 2022</td>
        <td>São Paulo</td>
        <td>SP</td>
        <td>Brazil</td>
        <td>01310-200</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>305</td>
        <td>55</td>
        <td>2012-08-31 00:00:00+00:00</td>
        <td>421 Bourke Street</td>
        <td>Sidney</td>
        <td>NSW</td>
        <td>Australia</td>
        <td>2010</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>388</td>
        <td>33</td>
        <td>2013-09-04 00:00:00+00:00</td>
        <td>5112 48 Street</td>
        <td>Yellowknife</td>
        <td>NT</td>
        <td>Canada</td>
        <td>X1A 1N6</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>18</td>
        <td>31</td>
        <td>2009-03-09 00:00:00+00:00</td>
        <td>194A Chain Lake Drive</td>
        <td>Halifax</td>
        <td>NS</td>
        <td>Canada</td>
        <td>B3S 1C5</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>255</td>
        <td>19</td>
        <td>2012-01-24 00:00:00+00:00</td>
        <td>1 Infinite Loop</td>
        <td>Cupertino</td>
        <td>CA</td>
        <td>USA</td>
        <td>95014</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>340</td>
        <td>9</td>
        <td>2013-02-02 00:00:00+00:00</td>
        <td>Sønder Boulevard 51</td>
        <td>Copenhagen</td>
        <td>None</td>
        <td>Denmark</td>
        <td>1720</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>310</td>
        <td>24</td>
        <td>2012-09-27 00:00:00+00:00</td>
        <td>162 E Superior Street</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>USA</td>
        <td>60611</td>
        <td>7.96</td>
    </tr>
    <tr>
        <td>186</td>
        <td>58</td>
        <td>2011-03-23 00:00:00+00:00</td>
        <td>12,Community Centre</td>
        <td>Delhi</td>
        <td>None</td>
        <td>India</td>
        <td>110017</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>80</td>
        <td>13</td>
        <td>2009-12-10 00:00:00+00:00</td>
        <td>Qe 7 Bloco G</td>
        <td>Brasília</td>
        <td>DF</td>
        <td>Brazil</td>
        <td>71020-677</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>360</td>
        <td>58</td>
        <td>2013-05-03 00:00:00+00:00</td>
        <td>12,Community Centre</td>
        <td>Delhi</td>
        <td>None</td>
        <td>India</td>
        <td>110017</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>31</td>
        <td>42</td>
        <td>2009-05-07 00:00:00+00:00</td>
        <td>9, Place Louis Barthou</td>
        <td>Bordeaux</td>
        <td>None</td>
        <td>France</td>
        <td>33000</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>325</td>
        <td>45</td>
        <td>2012-11-29 00:00:00+00:00</td>
        <td>Erzsébet krt. 58.</td>
        <td>Budapest</td>
        <td>None</td>
        <td>Hungary</td>
        <td>H-1073</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>333</td>
        <td>30</td>
        <td>2013-01-02 00:00:00+00:00</td>
        <td>230 Elgin Street</td>
        <td>Ottawa</td>
        <td>ON</td>
        <td>Canada</td>
        <td>K2P 1L7</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>277</td>
        <td>21</td>
        <td>2012-04-29 00:00:00+00:00</td>
        <td>801 W 4th Street</td>
        <td>Reno</td>
        <td>NV</td>
        <td>USA</td>
        <td>89503</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>115</td>
        <td>26</td>
        <td>2010-05-14 00:00:00+00:00</td>
        <td>2211 W Berry Street</td>
        <td>Fort Worth</td>
        <td>TX</td>
        <td>USA</td>
        <td>76110</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>402</td>
        <td>50</td>
        <td>2013-11-05 00:00:00+00:00</td>
        <td>C/ San Bernardo 85</td>
        <td>Madrid</td>
        <td>None</td>
        <td>Spain</td>
        <td>28015</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>200</td>
        <td>16</td>
        <td>2011-05-24 00:00:00+00:00</td>
        <td>1600 Amphitheatre Parkway</td>
        <td>Mountain View</td>
        <td>CA</td>
        <td>USA</td>
        <td>94043-1351</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>45</td>
        <td>59</td>
        <td>2009-07-08 00:00:00+00:00</td>
        <td>3,Raj Bhavan Road</td>
        <td>Bangalore</td>
        <td>None</td>
        <td>India</td>
        <td>560001</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>403</td>
        <td>56</td>
        <td>2013-11-08 00:00:00+00:00</td>
        <td>307 Macacha Güemes</td>
        <td>Buenos Aires</td>
        <td>None</td>
        <td>Argentina</td>
        <td>1106</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>368</td>
        <td>43</td>
        <td>2013-06-06 00:00:00+00:00</td>
        <td>68, Rue Jouvence</td>
        <td>Dijon</td>
        <td>None</td>
        <td>France</td>
        <td>21000</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>242</td>
        <td>8</td>
        <td>2011-11-26 00:00:00+00:00</td>
        <td>Grétrystraat 63</td>
        <td>Brussels</td>
        <td>None</td>
        <td>Belgium</td>
        <td>1000</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>136</td>
        <td>22</td>
        <td>2010-08-15 00:00:00+00:00</td>
        <td>120 S Orange Ave</td>
        <td>Orlando</td>
        <td>FL</td>
        <td>USA</td>
        <td>32801</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>410</td>
        <td>35</td>
        <td>2013-12-09 00:00:00+00:00</td>
        <td>Rua dos Campeões Europeus de Viena, 4350</td>
        <td>Porto</td>
        <td>None</td>
        <td>Portugal</td>
        <td>None</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>95</td>
        <td>36</td>
        <td>2010-02-13 00:00:00+00:00</td>
        <td>Tauentzienstraße 8</td>
        <td>Berlin</td>
        <td>None</td>
        <td>Germany</td>
        <td>10789</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>319</td>
        <td>13</td>
        <td>2012-11-01 00:00:00+00:00</td>
        <td>Qe 7 Bloco G</td>
        <td>Brasília</td>
        <td>DF</td>
        <td>Brazil</td>
        <td>71020-677</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>73</td>
        <td>34</td>
        <td>2009-11-09 00:00:00+00:00</td>
        <td>Rua da Assunção 53</td>
        <td>Lisbon</td>
        <td>None</td>
        <td>Portugal</td>
        <td>None</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>361</td>
        <td>5</td>
        <td>2013-05-06 00:00:00+00:00</td>
        <td>Klanova 9/506</td>
        <td>Prague</td>
        <td>None</td>
        <td>Czech Republic</td>
        <td>14700</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>241</td>
        <td>2</td>
        <td>2011-11-23 00:00:00+00:00</td>
        <td>Theodor-Heuss-Straße 34</td>
        <td>Stuttgart</td>
        <td>None</td>
        <td>Germany</td>
        <td>70174</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>101</td>
        <td>9</td>
        <td>2010-03-13 00:00:00+00:00</td>
        <td>Sønder Boulevard 51</td>
        <td>Copenhagen</td>
        <td>None</td>
        <td>Denmark</td>
        <td>1720</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>382</td>
        <td>1</td>
        <td>2013-08-07 00:00:00+00:00</td>
        <td>Av. Brigadeiro Faria Lima, 2170</td>
        <td>São José dos Campos</td>
        <td>SP</td>
        <td>Brazil</td>
        <td>12227-000</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>3</td>
        <td>8</td>
        <td>2009-01-03 00:00:00+00:00</td>
        <td>Grétrystraat 63</td>
        <td>Brussels</td>
        <td>None</td>
        <td>Belgium</td>
        <td>1000</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>381</td>
        <td>54</td>
        <td>2013-08-04 00:00:00+00:00</td>
        <td>110 Raeburn Pl</td>
        <td>Edinburgh </td>
        <td>None</td>
        <td>United Kingdom</td>
        <td>EH4 1HH</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>38</td>
        <td>21</td>
        <td>2009-06-07 00:00:00+00:00</td>
        <td>801 W 4th Street</td>
        <td>Reno</td>
        <td>NV</td>
        <td>USA</td>
        <td>89503</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>151</td>
        <td>45</td>
        <td>2010-10-19 00:00:00+00:00</td>
        <td>Erzsébet krt. 58.</td>
        <td>Budapest</td>
        <td>None</td>
        <td>Hungary</td>
        <td>H-1073</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>60</td>
        <td>23</td>
        <td>2009-09-11 00:00:00+00:00</td>
        <td>69 Salem Street</td>
        <td>Boston</td>
        <td>MA</td>
        <td>USA</td>
        <td>2113</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>228</td>
        <td>50</td>
        <td>2011-09-25 00:00:00+00:00</td>
        <td>C/ San Bernardo 85</td>
        <td>Madrid</td>
        <td>None</td>
        <td>Spain</td>
        <td>28015</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>227</td>
        <td>44</td>
        <td>2011-09-22 00:00:00+00:00</td>
        <td>Porthaninkatu 9</td>
        <td>Helsinki</td>
        <td>None</td>
        <td>Finland</td>
        <td>00530</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>137</td>
        <td>28</td>
        <td>2010-08-18 00:00:00+00:00</td>
        <td>302 S 700 E</td>
        <td>Salt Lake City</td>
        <td>UT</td>
        <td>USA</td>
        <td>84102</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>32</td>
        <td>48</td>
        <td>2009-05-10 00:00:00+00:00</td>
        <td>Lijnbaansgracht 120bg</td>
        <td>Amsterdam</td>
        <td>VV</td>
        <td>Netherlands</td>
        <td>1016</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>108</td>
        <td>47</td>
        <td>2010-04-13 00:00:00+00:00</td>
        <td>Via Degli Scipioni, 43</td>
        <td>Rome</td>
        <td>RM</td>
        <td>Italy</td>
        <td>00192</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>395</td>
        <td>12</td>
        <td>2013-10-05 00:00:00+00:00</td>
        <td>Praça Pio X, 119</td>
        <td>Rio de Janeiro</td>
        <td>RJ</td>
        <td>Brazil</td>
        <td>20040-020</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>87</td>
        <td>51</td>
        <td>2010-01-10 00:00:00+00:00</td>
        <td>Celsiusg. 9</td>
        <td>Stockholm</td>
        <td>None</td>
        <td>Sweden</td>
        <td>11230</td>
        <td>6.94</td>
    </tr>
    <tr>
        <td>206</td>
        <td>48</td>
        <td>2011-06-21 00:00:00+00:00</td>
        <td>Lijnbaansgracht 120bg</td>
        <td>Amsterdam</td>
        <td>VV</td>
        <td>Netherlands</td>
        <td>1016</td>
        <td>8.94</td>
    </tr>
    <tr>
        <td>122</td>
        <td>5</td>
        <td>2010-06-14 00:00:00+00:00</td>
        <td>Klanova 9/506</td>
        <td>Prague</td>
        <td>None</td>
        <td>Czech Republic</td>
        <td>14700</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>164</td>
        <td>56</td>
        <td>2010-12-17 00:00:00+00:00</td>
        <td>307 Macacha Güemes</td>
        <td>Buenos Aires</td>
        <td>None</td>
        <td>Argentina</td>
        <td>1106</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>221</td>
        <td>12</td>
        <td>2011-08-25 00:00:00+00:00</td>
        <td>Praça Pio X, 119</td>
        <td>Rio de Janeiro</td>
        <td>RJ</td>
        <td>Brazil</td>
        <td>20040-020</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>165</td>
        <td>3</td>
        <td>2010-12-20 00:00:00+00:00</td>
        <td>1498 rue Bélanger</td>
        <td>Montréal</td>
        <td>QC</td>
        <td>Canada</td>
        <td>H2G 1A7</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>249</td>
        <td>46</td>
        <td>2011-12-27 00:00:00+00:00</td>
        <td>3 Chatham Street</td>
        <td>Dublin</td>
        <td>Dublin</td>
        <td>Ireland</td>
        <td>None</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>207</td>
        <td>54</td>
        <td>2011-06-24 00:00:00+00:00</td>
        <td>110 Raeburn Pl</td>
        <td>Edinburgh </td>
        <td>None</td>
        <td>United Kingdom</td>
        <td>EH4 1HH</td>
        <td>8.91</td>
    </tr>
    <tr>
        <td>150</td>
        <td>39</td>
        <td>2010-10-16 00:00:00+00:00</td>
        <td>4, Rue Milton</td>
        <td>Paris</td>
        <td>None</td>
        <td>France</td>
        <td>75009</td>
        <td>5.94</td>
    </tr>
    <tr>
        <td>297</td>
        <td>11</td>
        <td>2012-07-28 00:00:00+00:00</td>
        <td>Av. Paulista, 2022</td>
        <td>São Paulo</td>
        <td>SP</td>
        <td>Brazil</td>
        <td>01310-200</td>
        <td>5.94</td>
    </tr>
</table>



## The set of all customers from USA, subtracted by the set of all customers with an email ending in 'yahoo.com'
the following command ask for all customers in the country USA, which does include everyone, but ask to exclude all that have a email that ends with yahoo.com with a exception clause.


```python
%sql (SELECT * from chinook.customer WHERE country = 'USA') except (SELECT * from chinook.customer WHERE email LIKE '%yahoo.com')
```

    11 rows affected.





<table>
    <tr>
        <th>customerid</th>
        <th>firstname</th>
        <th>lastname</th>
        <th>company</th>
        <th>address</th>
        <th>city</th>
        <th>state</th>
        <th>country</th>
        <th>postalcode</th>
        <th>phone</th>
        <th>fax</th>
        <th>email</th>
        <th>supportrepid</th>
    </tr>
    <tr>
        <td>21</td>
        <td>Kathy</td>
        <td>Chase</td>
        <td>None</td>
        <td>801 W 4th Street</td>
        <td>Reno</td>
        <td>NV</td>
        <td>USA</td>
        <td>89503</td>
        <td>+1 (775) 223-7665</td>
        <td>None</td>
        <td>kachase@hotmail.com</td>
        <td>5</td>
    </tr>
    <tr>
        <td>22</td>
        <td>Heather</td>
        <td>Leacock</td>
        <td>None</td>
        <td>120 S Orange Ave</td>
        <td>Orlando</td>
        <td>FL</td>
        <td>USA</td>
        <td>32801</td>
        <td>+1 (407) 999-7788</td>
        <td>None</td>
        <td>hleacock@gmail.com</td>
        <td>4</td>
    </tr>
    <tr>
        <td>16</td>
        <td>Frank</td>
        <td>Harris</td>
        <td>Google Inc.</td>
        <td>1600 Amphitheatre Parkway</td>
        <td>Mountain View</td>
        <td>CA</td>
        <td>USA</td>
        <td>94043-1351</td>
        <td>+1 (650) 253-0000</td>
        <td>+1 (650) 253-0000</td>
        <td>fharris@google.com</td>
        <td>4</td>
    </tr>
    <tr>
        <td>28</td>
        <td>Julia</td>
        <td>Barnett</td>
        <td>None</td>
        <td>302 S 700 E</td>
        <td>Salt Lake City</td>
        <td>UT</td>
        <td>USA</td>
        <td>84102</td>
        <td>+1 (801) 531-7272</td>
        <td>None</td>
        <td>jubarnett@gmail.com</td>
        <td>5</td>
    </tr>
    <tr>
        <td>19</td>
        <td>Tim</td>
        <td>Goyer</td>
        <td>Apple Inc.</td>
        <td>1 Infinite Loop</td>
        <td>Cupertino</td>
        <td>CA</td>
        <td>USA</td>
        <td>95014</td>
        <td>+1 (408) 996-1010</td>
        <td>+1 (408) 996-1011</td>
        <td>tgoyer@apple.com</td>
        <td>3</td>
    </tr>
    <tr>
        <td>18</td>
        <td>Michelle</td>
        <td>Brooks</td>
        <td>None</td>
        <td>627 Broadway</td>
        <td>New York</td>
        <td>NY</td>
        <td>USA</td>
        <td>10012-2612</td>
        <td>+1 (212) 221-3546</td>
        <td>+1 (212) 221-4679</td>
        <td>michelleb@aol.com</td>
        <td>3</td>
    </tr>
    <tr>
        <td>17</td>
        <td>Jack</td>
        <td>Smith</td>
        <td>Microsoft Corporation</td>
        <td>1 Microsoft Way</td>
        <td>Redmond</td>
        <td>WA</td>
        <td>USA</td>
        <td>98052-8300</td>
        <td>+1 (425) 882-8080</td>
        <td>+1 (425) 882-8081</td>
        <td>jacksmith@microsoft.com</td>
        <td>5</td>
    </tr>
    <tr>
        <td>26</td>
        <td>Richard</td>
        <td>Cunningham</td>
        <td>None</td>
        <td>2211 W Berry Street</td>
        <td>Fort Worth</td>
        <td>TX</td>
        <td>USA</td>
        <td>76110</td>
        <td>+1 (817) 924-7272</td>
        <td>None</td>
        <td>ricunningham@hotmail.com</td>
        <td>4</td>
    </tr>
    <tr>
        <td>20</td>
        <td>Dan</td>
        <td>Miller</td>
        <td>None</td>
        <td>541 Del Medio Avenue</td>
        <td>Mountain View</td>
        <td>CA</td>
        <td>USA</td>
        <td>94040-111</td>
        <td>+1 (650) 644-3358</td>
        <td>None</td>
        <td>dmiller@comcast.com</td>
        <td>4</td>
    </tr>
    <tr>
        <td>27</td>
        <td>Patrick</td>
        <td>Gray</td>
        <td>None</td>
        <td>1033 N Park Ave</td>
        <td>Tucson</td>
        <td>AZ</td>
        <td>USA</td>
        <td>85719</td>
        <td>+1 (520) 622-4200</td>
        <td>None</td>
        <td>patrick.gray@aol.com</td>
        <td>4</td>
    </tr>
    <tr>
        <td>24</td>
        <td>Frank</td>
        <td>Ralston</td>
        <td>None</td>
        <td>162 E Superior Street</td>
        <td>Chicago</td>
        <td>IL</td>
        <td>USA</td>
        <td>60611</td>
        <td>+1 (312) 332-3232</td>
        <td>None</td>
        <td>fralston@gmail.com</td>
        <td>3</td>
    </tr>
</table>



## The union of the set of all albums playing something by Mozart and the set of all albums playing something with Bach
the following code selects all albums where a albumid in a track composed by mozart is shared with the album, then take the union of the same command with the difference being sebastion bach.


```python
%sql (SELECT * from chinook.album WHERE albumid in (SELECT albumid from Chinook.track WHERE composer LIKE '%Moz%')) UNION (SELECT * from chinook.album WHERE albumid in (SELECT albumid from chinook.track WHERE composer LIKE '%Sebastian Bach%'))
```

    12 rows affected.





<table>
    <tr>
        <th>albumid</th>
        <th>title</th>
        <th>artistid</th>
    </tr>
    <tr>
        <td>317</td>
        <td>Mozart Gala: Famous Arias</td>
        <td>249</td>
    </tr>
    <tr>
        <td>297</td>
        <td>Bach: Toccata &amp; Fugue in D Minor</td>
        <td>231</td>
    </tr>
    <tr>
        <td>335</td>
        <td>J.S. Bach: Chaconne, Suite in E Minor, Partita in E Major &amp; Prelude, Fugue and Allegro</td>
        <td>265</td>
    </tr>
    <tr>
        <td>327</td>
        <td>Bach: Orchestral Suites Nos. 1 - 4</td>
        <td>257</td>
    </tr>
    <tr>
        <td>320</td>
        <td>Mozart: Symphonies Nos. 40 &amp; 41</td>
        <td>248</td>
    </tr>
    <tr>
        <td>278</td>
        <td>Bach: The Cello Suites</td>
        <td>212</td>
    </tr>
    <tr>
        <td>277</td>
        <td>Bach: Goldberg Variations</td>
        <td>211</td>
    </tr>
    <tr>
        <td>346</td>
        <td>Mozart: Chamber Music</td>
        <td>274</td>
    </tr>
    <tr>
        <td>276</td>
        <td>Bach: Violin Concertos</td>
        <td>210</td>
    </tr>
    <tr>
        <td>300</td>
        <td>Bach: The Brandenburg Concertos</td>
        <td>234</td>
    </tr>
    <tr>
        <td>282</td>
        <td>Mozart: Wind Concertos</td>
        <td>216</td>
    </tr>
    <tr>
        <td>281</td>
        <td>Sir Neville Marriner: A Celebration</td>
        <td>215</td>
    </tr>
</table>


