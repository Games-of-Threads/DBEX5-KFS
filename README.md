
# DBEX5-KFS
> by kristian flejsborg sørensen (cph-kf96)


```python
%load_ext sql
```


```python
%sql postgresql://appdev@192.168.33.10/appdev
```




    'Connected: appdev@appdev'



## 1
On the table circuits report:
1. What type of indices exists for the table and why they are of that type (and not some other type)   
2. The amount of space each index takes up

the following pictures showcases the indicies of the circuits table, 2 of them are B-tree on url and circuitID respectively, and the last is a generalised search tree on the position.   

the url is a http link, which works best with the B-tree's multiple leaves structure, although R-tree's allows for overlapping sites of the same link with minor differences, B-tree's is log(n) to search and R-tree's is log m (n) being slightly slower, BRIN and Bloom don't make much senses as it's just a http link.   
the same can be said about circuitID as they both implement the unique constraint.   

the position is a different matter, as it isn't using the unique constraint, and a point which is a 16 bytes (x,y) value, while the table also containts a latitude and longtidude using double precision which are 8 bytes each for the same total, I hazard a geuss that the redundant point value is used to index the cordinates in a easy way, though I question the reason for having the two other values in this regard. the reason a R-tree isn't used is mostly because the point doesn't explain a area but a singular position, and the GIST tree allow for easy management and fast searching for the data.   
the GIST tree does require more space to be indexed, going from 16 byte per row to a single 8192 byte index, which is alot more than the 584 byte total it was without the index.

![](https://i.gyazo.com/b896b362824d4fed541177c9ae79c1d7.png)   
![](https://i.gyazo.com/4634dd4fb50968033838f6001f8b9f7d.png)

related data shown below.


```python
%sql select * from pg_indexes where tablename = 'circuits';
```

    3 rows affected.





<table>
    <tr>
        <th>schemaname</th>
        <th>tablename</th>
        <th>indexname</th>
        <th>tablespace</th>
        <th>indexdef</th>
    </tr>
    <tr>
        <td>f1db</td>
        <td>circuits</td>
        <td>idx_17102_url</td>
        <td>None</td>
        <td>CREATE UNIQUE INDEX idx_17102_url ON circuits USING btree (url)</td>
    </tr>
    <tr>
        <td>f1db</td>
        <td>circuits</td>
        <td>circuits_position_idx</td>
        <td>None</td>
        <td>CREATE INDEX circuits_position_idx ON circuits USING gist (&quot;position&quot;)</td>
    </tr>
    <tr>
        <td>f1db</td>
        <td>circuits</td>
        <td>idx_17102_primary</td>
        <td>None</td>
        <td>CREATE UNIQUE INDEX idx_17102_primary ON circuits USING btree (circuitid)</td>
    </tr>
</table>




```python
%sql select * from information_schema.columns where table_schema = 'f1db' and table_name = 'circuits';
```

    10 rows affected.





<table>
    <tr>
        <th>table_catalog</th>
        <th>table_schema</th>
        <th>table_name</th>
        <th>column_name</th>
        <th>ordinal_position</th>
        <th>column_default</th>
        <th>is_nullable</th>
        <th>data_type</th>
        <th>character_maximum_length</th>
        <th>character_octet_length</th>
        <th>numeric_precision</th>
        <th>numeric_precision_radix</th>
        <th>numeric_scale</th>
        <th>datetime_precision</th>
        <th>interval_type</th>
        <th>interval_precision</th>
        <th>character_set_catalog</th>
        <th>character_set_schema</th>
        <th>character_set_name</th>
        <th>collation_catalog</th>
        <th>collation_schema</th>
        <th>collation_name</th>
        <th>domain_catalog</th>
        <th>domain_schema</th>
        <th>domain_name</th>
        <th>udt_catalog</th>
        <th>udt_schema</th>
        <th>udt_name</th>
        <th>scope_catalog</th>
        <th>scope_schema</th>
        <th>scope_name</th>
        <th>maximum_cardinality</th>
        <th>dtd_identifier</th>
        <th>is_self_referencing</th>
        <th>is_identity</th>
        <th>identity_generation</th>
        <th>identity_start</th>
        <th>identity_increment</th>
        <th>identity_maximum</th>
        <th>identity_minimum</th>
        <th>identity_cycle</th>
        <th>is_generated</th>
        <th>generation_expression</th>
        <th>is_updatable</th>
    </tr>
    <tr>
        <td>appdev</td>
        <td>f1db</td>
        <td>circuits</td>
        <td>circuitid</td>
        <td>1</td>
        <td>nextval(&#x27;circuits_circuitid_seq&#x27;::regclass)</td>
        <td>NO</td>
        <td>bigint</td>
        <td>None</td>
        <td>None</td>
        <td>64</td>
        <td>2</td>
        <td>0</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>appdev</td>
        <td>pg_catalog</td>
        <td>int8</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>1</td>
        <td>NO</td>
        <td>NO</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NO</td>
        <td>NEVER</td>
        <td>None</td>
        <td>YES</td>
    </tr>
    <tr>
        <td>appdev</td>
        <td>f1db</td>
        <td>circuits</td>
        <td>circuitref</td>
        <td>2</td>
        <td>&#x27;&#x27;::character varying</td>
        <td>NO</td>
        <td>character varying</td>
        <td>255</td>
        <td>1020</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>appdev</td>
        <td>pg_catalog</td>
        <td>varchar</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>2</td>
        <td>NO</td>
        <td>NO</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NO</td>
        <td>NEVER</td>
        <td>None</td>
        <td>YES</td>
    </tr>
    <tr>
        <td>appdev</td>
        <td>f1db</td>
        <td>circuits</td>
        <td>name</td>
        <td>3</td>
        <td>&#x27;&#x27;::character varying</td>
        <td>NO</td>
        <td>character varying</td>
        <td>255</td>
        <td>1020</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>appdev</td>
        <td>pg_catalog</td>
        <td>varchar</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>3</td>
        <td>NO</td>
        <td>NO</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NO</td>
        <td>NEVER</td>
        <td>None</td>
        <td>YES</td>
    </tr>
    <tr>
        <td>appdev</td>
        <td>f1db</td>
        <td>circuits</td>
        <td>location</td>
        <td>4</td>
        <td>NULL::character varying</td>
        <td>YES</td>
        <td>character varying</td>
        <td>255</td>
        <td>1020</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>appdev</td>
        <td>pg_catalog</td>
        <td>varchar</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>4</td>
        <td>NO</td>
        <td>NO</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NO</td>
        <td>NEVER</td>
        <td>None</td>
        <td>YES</td>
    </tr>
    <tr>
        <td>appdev</td>
        <td>f1db</td>
        <td>circuits</td>
        <td>country</td>
        <td>5</td>
        <td>NULL::character varying</td>
        <td>YES</td>
        <td>character varying</td>
        <td>255</td>
        <td>1020</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>appdev</td>
        <td>pg_catalog</td>
        <td>varchar</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>5</td>
        <td>NO</td>
        <td>NO</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NO</td>
        <td>NEVER</td>
        <td>None</td>
        <td>YES</td>
    </tr>
    <tr>
        <td>appdev</td>
        <td>f1db</td>
        <td>circuits</td>
        <td>lat</td>
        <td>6</td>
        <td>None</td>
        <td>YES</td>
        <td>double precision</td>
        <td>None</td>
        <td>None</td>
        <td>53</td>
        <td>2</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>appdev</td>
        <td>pg_catalog</td>
        <td>float8</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>6</td>
        <td>NO</td>
        <td>NO</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NO</td>
        <td>NEVER</td>
        <td>None</td>
        <td>YES</td>
    </tr>
    <tr>
        <td>appdev</td>
        <td>f1db</td>
        <td>circuits</td>
        <td>lng</td>
        <td>7</td>
        <td>None</td>
        <td>YES</td>
        <td>double precision</td>
        <td>None</td>
        <td>None</td>
        <td>53</td>
        <td>2</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>appdev</td>
        <td>pg_catalog</td>
        <td>float8</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>7</td>
        <td>NO</td>
        <td>NO</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NO</td>
        <td>NEVER</td>
        <td>None</td>
        <td>YES</td>
    </tr>
    <tr>
        <td>appdev</td>
        <td>f1db</td>
        <td>circuits</td>
        <td>alt</td>
        <td>8</td>
        <td>None</td>
        <td>YES</td>
        <td>bigint</td>
        <td>None</td>
        <td>None</td>
        <td>64</td>
        <td>2</td>
        <td>0</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>appdev</td>
        <td>pg_catalog</td>
        <td>int8</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>8</td>
        <td>NO</td>
        <td>NO</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NO</td>
        <td>NEVER</td>
        <td>None</td>
        <td>YES</td>
    </tr>
    <tr>
        <td>appdev</td>
        <td>f1db</td>
        <td>circuits</td>
        <td>url</td>
        <td>9</td>
        <td>&#x27;&#x27;::character varying</td>
        <td>NO</td>
        <td>character varying</td>
        <td>255</td>
        <td>1020</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>appdev</td>
        <td>pg_catalog</td>
        <td>varchar</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>9</td>
        <td>NO</td>
        <td>NO</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NO</td>
        <td>NEVER</td>
        <td>None</td>
        <td>YES</td>
    </tr>
    <tr>
        <td>appdev</td>
        <td>f1db</td>
        <td>circuits</td>
        <td>position</td>
        <td>10</td>
        <td>None</td>
        <td>YES</td>
        <td>point</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>appdev</td>
        <td>pg_catalog</td>
        <td>point</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>10</td>
        <td>NO</td>
        <td>NO</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>NO</td>
        <td>NEVER</td>
        <td>None</td>
        <td>YES</td>
    </tr>
</table>



## 2
We are talent scouts looking to win over some of the best new drivers there are. But we don't want them too old! Write a query that finds the winner of all the races, but only if they are younger than 38 years. The query should give return the date, driver surname, driver age, track time in milliseconds, race name and circuit name for all races.

the following query achives this, note LIMIT is used to keep this from getting too long as there are 184 hits.


```python
%%sql
SELECT date, drivers.surname, EXTRACT(YEAR FROM now())-EXTRACT(YEAR FROM drivers.dob) 
as DriversAge, milliseconds, races.name as RaceName, circuits.name as CircuitName FROM races
JOIN circuits ON circuits.circuitid = races.circuitid
JOIN results ON results.raceid = races.raceid AND results.position = 1 
JOIN drivers USING (driverid) WHERE drivers.dob + interval '38 years' > now() 
ORDER BY date DESC LIMIT 10;
```

    10 rows affected.





<table>
    <tr>
        <th>date</th>
        <th>surname</th>
        <th>driversage</th>
        <th>milliseconds</th>
        <th>racename</th>
        <th>circuitname</th>
    </tr>
    <tr>
        <td>2017-10-01</td>
        <td>Verstappen</td>
        <td>21.0</td>
        <td>5401290</td>
        <td>Malaysian Grand Prix</td>
        <td>Sepang International Circuit</td>
    </tr>
    <tr>
        <td>2017-09-17</td>
        <td>Hamilton</td>
        <td>33.0</td>
        <td>7403544</td>
        <td>Singapore Grand Prix</td>
        <td>Marina Bay Street Circuit</td>
    </tr>
    <tr>
        <td>2017-09-03</td>
        <td>Hamilton</td>
        <td>33.0</td>
        <td>4532312</td>
        <td>Italian Grand Prix</td>
        <td>Autodromo Nazionale di Monza</td>
    </tr>
    <tr>
        <td>2017-08-27</td>
        <td>Hamilton</td>
        <td>33.0</td>
        <td>5082820</td>
        <td>Belgian Grand Prix</td>
        <td>Circuit de Spa-Francorchamps</td>
    </tr>
    <tr>
        <td>2017-07-30</td>
        <td>Vettel</td>
        <td>31.0</td>
        <td>5986713</td>
        <td>Hungarian Grand Prix</td>
        <td>Hungaroring</td>
    </tr>
    <tr>
        <td>2017-07-16</td>
        <td>Hamilton</td>
        <td>33.0</td>
        <td>4887430</td>
        <td>British Grand Prix</td>
        <td>Silverstone Circuit</td>
    </tr>
    <tr>
        <td>2017-07-09</td>
        <td>Bottas</td>
        <td>29.0</td>
        <td>4908523</td>
        <td>Austrian Grand Prix</td>
        <td>Red Bull Ring</td>
    </tr>
    <tr>
        <td>2017-06-25</td>
        <td>Ricciardo</td>
        <td>29.0</td>
        <td>7435573</td>
        <td>Azerbaijan Grand Prix</td>
        <td>Baku City Circuit</td>
    </tr>
    <tr>
        <td>2017-06-11</td>
        <td>Hamilton</td>
        <td>33.0</td>
        <td>5585154</td>
        <td>Canadian Grand Prix</td>
        <td>Circuit Gilles Villeneuve</td>
    </tr>
    <tr>
        <td>2017-05-28</td>
        <td>Vettel</td>
        <td>31.0</td>
        <td>6284340</td>
        <td>Monaco Grand Prix</td>
        <td>Circuit de Monaco</td>
    </tr>
</table>



## 3
Describe the query using EXPLAIN ANALYZE with at least 5 lines of text. Answer at least the following:
How many calls are you making?
How long does it take to perform the query?

note the following query is used without LIMIT to get the correct results.   
it starts out with the initial 3 values, and sorts by races.date as defined in the end of the query, it then proceeds to join the races table with the circuits table using the shared circuitid attribute thats between them, it then proceeds to join the results table using the shared raceid attribute that the races table and results table shares, it then joins the last table drivers on the driverid that drivers and results shares.   

after all that it starts to filter all the irrelevant data, by filtering out all tables where results.position isn't 1 effectively removing 22703 rows. Next it filters based on date of birth between now and 38 years effectively removing 781 additional old timers.

it starts out scanning circuits which is the table it intends to join on the races table, going through 73 rows of data, it then saves this data locally as hash data and proceeds, it does this again with the races and goes through it's 976 rows, then it filters out the rows that don't correspond with the id's of the respective tables.   

it's unknown to me the effect and cause of the scans afterwards.


```python
%%sql EXPLAIN ANALYZE
SELECT date, drivers.surname, EXTRACT(YEAR FROM now())-EXTRACT(YEAR FROM drivers.dob) as DriversAge, milliseconds, races.name as RaceName, circuits.name as CircuitName FROM races
JOIN circuits ON circuits.circuitid = races.circuitid
JOIN results ON results.raceid = races.raceid AND results.position = 1 
JOIN drivers USING (driverid) WHERE drivers.dob + interval '38 years' > now() 
ORDER BY date DESC;
```

    25 rows affected.





<table>
    <tr>
        <th>QUERY PLAN</th>
    </tr>
    <tr>
        <td>Sort  (cost=822.78..823.59 rows=324 width=66) (actual time=2.340..2.348 rows=184 loops=1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;Sort Key: races.date DESC</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;Sort Method: quicksort  Memory: 50kB</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;-&gt;  Hash Join  (cost=75.82..809.27 rows=324 width=66) (actual time=0.395..2.294 rows=184 loops=1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hash Cond: (races.circuitid = circuits.circuitid)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&gt;  Hash Join  (cost=72.18..797.52 rows=324 width=50) (actual time=0.368..2.211 rows=184 loops=1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hash Cond: (results.raceid = races.raceid)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&gt;  Hash Join  (cost=32.22..753.47 rows=324 width=27) (actual time=0.140..1.950 rows=184 loops=1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hash Cond: (results.driverid = drivers.driverid)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&gt;  Seq Scan on results  (cost=0.00..708.96 rows=974 width=24) (actual time=0.002..1.696 rows=974 loops=1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Filter: (&quot;position&quot; = 1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Rows Removed by Filter: 22703</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&gt;  Hash  (cost=28.72..28.72 rows=280 width=19) (actual time=0.134..0.134 rows=60 loops=1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Buckets: 1024  Batches: 1  Memory Usage: 12kB</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&gt;  Seq Scan on drivers  (cost=0.00..28.72 rows=280 width=19) (actual time=0.003..0.125 rows=60 loops=1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Filter: ((dob + &#x27;38 years&#x27;::interval) &gt; now())</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Rows Removed by Filter: 781</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&gt;  Hash  (cost=27.76..27.76 rows=976 width=39) (actual time=0.224..0.224 rows=976 loops=1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Buckets: 1024  Batches: 1  Memory Usage: 79kB</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&gt;  Seq Scan on races  (cost=0.00..27.76 rows=976 width=39) (actual time=0.002..0.102 rows=976 loops=1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&gt;  Hash  (cost=2.73..2.73 rows=73 width=28) (actual time=0.021..0.021 rows=73 loops=1)</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Buckets: 1024  Batches: 1  Memory Usage: 13kB</td>
    </tr>
    <tr>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&gt;  Seq Scan on circuits  (cost=0.00..2.73 rows=73 width=28) (actual time=0.004..0.011 rows=73 loops=1)</td>
    </tr>
    <tr>
        <td>Planning time: 0.299 ms</td>
    </tr>
    <tr>
        <td>Execution time: 2.391 ms</td>
    </tr>
</table>



## 4
Create a materialized view of your query. Using EXPLAIN ANALYZE try to query the view. Write at least 5 lines of text explaining what's going on and why the query execution time changed.

before the materialized view the planning took 0.3 miliseconds for postgresql to plan the query and 2.4 miliseconds to execute for a total of 2.7 miliseconds.   
The materialised view saves the query results in memory allowing for quick and easy use, however a materialized view is a static snapshot of the data at the time of creating the view, the benefit is the speed, as planning now takes 0.02 miliseconds, and execution time is 0.03 for a total of 0.05 milisecond compared to 2.7 miliseconds.


```python
%%sql
CREATE MATERIALIZED VIEW race_winners_cache AS
SELECT date, drivers.surname, EXTRACT(YEAR FROM now())-EXTRACT(YEAR FROM drivers.dob) as DriversAge, milliseconds, races.name as RaceName, circuits.name as CircuitName FROM races
JOIN circuits ON circuits.circuitid = races.circuitid
JOIN results ON results.raceid = races.raceid AND results.position = 1 
JOIN drivers USING (driverid) WHERE drivers.dob + interval '38 years' > now() 
ORDER BY date DESC;
```

    184 rows affected.





    []




```python
%sql select * from race_winners_cache LIMIT 10
```

    10 rows affected.





<table>
    <tr>
        <th>date</th>
        <th>surname</th>
        <th>driversage</th>
        <th>milliseconds</th>
        <th>racename</th>
        <th>circuitname</th>
    </tr>
    <tr>
        <td>2017-10-01</td>
        <td>Verstappen</td>
        <td>21.0</td>
        <td>5401290</td>
        <td>Malaysian Grand Prix</td>
        <td>Sepang International Circuit</td>
    </tr>
    <tr>
        <td>2017-09-17</td>
        <td>Hamilton</td>
        <td>33.0</td>
        <td>7403544</td>
        <td>Singapore Grand Prix</td>
        <td>Marina Bay Street Circuit</td>
    </tr>
    <tr>
        <td>2017-09-03</td>
        <td>Hamilton</td>
        <td>33.0</td>
        <td>4532312</td>
        <td>Italian Grand Prix</td>
        <td>Autodromo Nazionale di Monza</td>
    </tr>
    <tr>
        <td>2017-08-27</td>
        <td>Hamilton</td>
        <td>33.0</td>
        <td>5082820</td>
        <td>Belgian Grand Prix</td>
        <td>Circuit de Spa-Francorchamps</td>
    </tr>
    <tr>
        <td>2017-07-30</td>
        <td>Vettel</td>
        <td>31.0</td>
        <td>5986713</td>
        <td>Hungarian Grand Prix</td>
        <td>Hungaroring</td>
    </tr>
    <tr>
        <td>2017-07-16</td>
        <td>Hamilton</td>
        <td>33.0</td>
        <td>4887430</td>
        <td>British Grand Prix</td>
        <td>Silverstone Circuit</td>
    </tr>
    <tr>
        <td>2017-07-09</td>
        <td>Bottas</td>
        <td>29.0</td>
        <td>4908523</td>
        <td>Austrian Grand Prix</td>
        <td>Red Bull Ring</td>
    </tr>
    <tr>
        <td>2017-06-25</td>
        <td>Ricciardo</td>
        <td>29.0</td>
        <td>7435573</td>
        <td>Azerbaijan Grand Prix</td>
        <td>Baku City Circuit</td>
    </tr>
    <tr>
        <td>2017-06-11</td>
        <td>Hamilton</td>
        <td>33.0</td>
        <td>5585154</td>
        <td>Canadian Grand Prix</td>
        <td>Circuit Gilles Villeneuve</td>
    </tr>
    <tr>
        <td>2017-05-28</td>
        <td>Vettel</td>
        <td>31.0</td>
        <td>6284340</td>
        <td>Monaco Grand Prix</td>
        <td>Circuit de Monaco</td>
    </tr>
</table>




```python
%sql EXPLAIN ANALYZE select * from race_winners_cache 
```

    3 rows affected.





<table>
    <tr>
        <th>QUERY PLAN</th>
    </tr>
    <tr>
        <td>Seq Scan on race_winners_cache  (cost=0.00..4.84 rows=184 width=69) (actual time=0.005..0.017 rows=184 loops=1)</td>
    </tr>
    <tr>
        <td>Planning time: 0.018 ms</td>
    </tr>
    <tr>
        <td>Execution time: 0.031 ms</td>
    </tr>
</table>


