


{:.no_toc}
* toc
{:toc}


Speech-to-SQL (S2SQL) aims to convert spo002 ken questions into SQL queries given relational databases, which has been traditionally implemented in a cascaded manner while facing the following challenges: 1) model training is faced with the major issue of data scarcity, where limited parallel data is available; and 2) the systems should differ from the source data. In this work, we propose the first direct speech-to-SQL parsing model Wav2SQL which avoids error compounding across cascaded systems. Specifically, 1) to accelerate speech-driven SQL parsing research in the community, we release a large-scale and multi-speaker dataset MASpider; 2) leveraging the recent progress in the large-scale pre-training, we show that it alleviates the data scarcity issue and allow for di020 rect speech-to-SQL parsing; and 3) we include the speech re-programming and gradient reversal classifier techniques to reduce acoustic variance and learned style-agnostic representa024 tion, improving generalization to unseen out-of-domain custom data. Experimental results demonstrate that Wav2SQL avoids error compounding and achieves state-of-the-art results by up to 4.6% accuracy improvement over the baseline.


Audio samples are available at <a href="https://Wav2SQL.github.io/"><i>https://Wav2SQL.github.io/</i></a>.

<br>

# Wav2SQL: Direct Generalizable Speech-To-SQL Parsing
## Britian Accent

<br>

<table>
        <!-- <tr>
            <th></th>
            <th colspan="2">Ground truth</th>
            <th colspan="3">Predictions</th>
        </tr> -->
        <tr>
            <th></th>
            <th>Spoken question</th>
            <th>Text question</th>
            <th>Target SQL</th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 1: </th>
        </tr> -->
        <tr>
            <th>Male Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK008-M-British/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>What are the names of projects that require more than 300 hours, and how many scientists are assigned to each?</td>
           </th>
           <th>
                <td>SELECT count(*) ,  T1.name FROM projects AS T1 JOIN assignedto AS T2 ON T1.code  =  T2.project WHERE T1.hours  >  300 GROUP BY T1.name</td>
           </th>
        </tr>
        <tr>
            <th>Male Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK008-M-British/001.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>Find the number of projects which each scientist is working on and scientist's name.</td>
           </th>
           <th>
                <td>SELECT count(*) ,  T1.name FROM scientists AS T1 JOIN assignedto AS T2 ON T1.ssn  =  T2.scientist GROUP BY T1.name</td>
           </th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 2: </th>
        </tr> -->
        <tr>
            <th>Female Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK007-F-British/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>Find the emails of customers who has filed a complaints of the product with the most complaints.</td>
           </th>
           <th>
                <td>SELECT t1.email_address FROM customers AS t1 JOIN complaints AS t2 ON t1.customer_id  =  t2.customer_id GROUP BY t1.customer_id ORDER BY count(*) LIMIT 1</td>
           </th>
        </tr>
        <tr>
            <th>Female Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK007-F-British/002.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>Which products has been complained by the customer who has filed least amount of complaints?</td>
           </th>
           <th>
                <td>SELECT DISTINCT t1.product_name FROM products AS t1 JOIN complaints AS t2 ON t1.product_id  =  t2.product_id JOIN customers AS t3 GROUP BY t3.customer_id ORDER BY count(*) LIMIT 1</td>
           </th>
        </tr>
</table>

<br/>

## Japan Accent

<br>

<table>
        <!-- <tr>
            <th></th>
            <th colspan="2">Ground truth</th>
            <th colspan="3">Predictions</th>
        </tr> -->
        <tr>
            <th></th>
            <th>Spoken question</th>
            <th>Text question</th>
            <th>Target SQL</th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 1: </th>
        </tr> -->
        <tr>
            <th>Male Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK006-M-Japan/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>What are the carriers of devices whose software platforms are not "Android"?</td>
           </th>
           <th>
                <td>SELECT Carrier FROM device WHERE Software_Platform != 'Android'</td>
           </th>
        </tr>
        <tr>
            <th>Male Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK006-M-Japan/002.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>What are the names of shops in ascending order of open year?</td>
           </th>
           <th>
                <td>SELECT Shop_Name FROM shop ORDER BY Open_Year ASC</td>
           </th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 2: </th>
        </tr> -->
        <tr>
            <th>Female Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK005-F-Japan/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>How many friends does Dan have?</td>
           </th>
           <th>
                <td>SELECT count(T2.friend) FROM Person AS T1 JOIN PersonFriend AS T2 ON T1.name  =  T2.name WHERE T1.name  =  'Dan'</td>
           </th>
        </tr>
        <tr>
            <th>Female Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK005-F-Japan/001.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>How many females does this network has?</td>
           </th>
           <th>
                <td>SELECT count(*) FROM Person WHERE gender  =  'female'</td>
           </th>
        </tr>
</table>


<br>

## Thailand Accent

<br>

<table>
        <!-- <tr>
            <th></th>
            <th colspan="2">Ground truth</th>
            <th colspan="3">Predictions</th>
        </tr> -->
        <tr>
            <th></th>
            <th>Spoken question</th>
            <th>Text question</th>
            <th>Target SQL</th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 1: </th>
        </tr> -->
        <tr>
            <th>Male Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK002-M-Thailand/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>What is the forename and surname of the driver with the shortest laptime?</td>
           </th>
           <th>
                <td>SELECT T1.forename ,  T1.surname FROM drivers AS T1 JOIN laptimes AS T2 ON T1.driverid = T2.driverid ORDER BY T2.milliseconds LIMIT 1</td>
           </th>
        </tr>
        <tr>
            <th>Male Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK002-M-Thailand/001.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>What is the id and family name of the driver who has the longest laptime?</td>
           </th>
           <th>
                <td>SELECT T1.driverid ,  T1.surname FROM drivers AS T1 JOIN laptimes AS T2 ON T1.driverid = T2.driverid ORDER BY T2.milliseconds DESC LIMIT 1</td>
           </th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 2: </th>
        </tr> -->
        <tr>
            <th>Female Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK001-F-Thailand/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>Find the buildings which have rooms with capacity more than 50.</td>
           </th>
           <th>
                <td>SELECT DISTINCT building FROM classroom WHERE capacity  >  50</td>
           </th>
        </tr>
        <tr>
            <th>Female Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK001-F-Thailand/002.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>Count the number of rooms that are not in the Lamberton building.</td>
           </th>
           <th>
                <td>SELECT count(*) FROM classroom WHERE building != 'Lamberton'</td>
           </th>
        </tr>
</table>

<br>

## China Accent

<br>

<table>
        <!-- <tr>
            <th></th>
            <th colspan="2">Ground truth</th>
            <th colspan="3">Predictions</th>
        </tr> -->
        <tr>
            <th></th>
            <th>Spoken question</th>
            <th>Text question</th>
            <th>Target SQL</th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 1: </th>
        </tr> -->
        <tr>
            <th>Male Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK010-M-China/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>how long is rio grande</td>
           </th>
           <th>
                <td>SELECT LENGTH FROM river WHERE river_name = "rio grande"</td>
           </th>
        </tr>
        <tr>
            <th>Male Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK010-M-China/001.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>how long is the longest river in texas</td>
           </th>
           <th>
                <td>SELECT LENGTH FROM river WHERE LENGTH = ( SELECT MAX ( LENGTH ) FROM river WHERE traverse = "texas" ) AND traverse = "texas"</td>
           </th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 2: </th>
        </tr> -->
        <tr>
            <th>Female Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK009-F-China/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>How many papers did michael i. jordan publish in 2016 ?</td>
           </th>
           <th>
                <td>SELECT DISTINCT COUNT ( t2.paperid ) FROM writes AS t2 JOIN author AS t1 ON t2.authorid = t1.authorid JOIN paper AS t3 ON t2.paperid = t3.paperid WHERE t1.authorname = "michael i. jordan" AND t3.year = 2016</td>
           </th>
        </tr>
        <tr>
            <th>Female Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK009-F-China/001.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>How many papers did michael i. jordan publish in 2016 ?</td>
           </th>
           <th>
                <td>SELECT DISTINCT COUNT ( t2.paperid ) FROM writes AS t2 JOIN author AS t1 ON t2.authorid = t1.authorid JOIN paper AS t3 ON t2.paperid = t3.paperid WHERE t1.authorname = "michael i. jordan" AND t3.year = 2016</td>
           </th>
        </tr>
</table>

<br>

## America Accent

<br>

<table>
        <!-- <tr>
            <th></th>
            <th colspan="2">Ground truth</th>
            <th colspan="3">Predictions</th>
        </tr> -->
        <tr>
            <th></th>
            <th>Spoken question</th>
            <th>Text question</th>
            <th>Target SQL</th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 1: </th>
        </tr> -->
        <tr>
            <th>Male Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK004-M-America/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>How many heads of the departments are older than 56 ?</td>
           </th>
           <th>
                <td>SELECT count(*) FROM head WHERE age  >  56</td>
           </th>
        </tr>
        <tr>
            <th>Male Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK004-M-America/001.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>List the name, born state and age of the heads of departments ordered by age.</td>
           </th>
           <th>
                <td>SELECT name, born_state, age FROM head ORDER BY age</td>
           </th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 2: </th>
        </tr> -->
        <tr>
            <th>Female Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK003-F-America/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>Give me the dates when the max temperature was higher than 85.</td>
           </th>
           <th>
                <td>SELECT date FROM weather WHERE max_temperature_f > 85</td>
           </th>
        </tr>
        <tr>
            <th>Female Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK003-F-America/002.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>What are the names of stations that have latitude lower than 37.5?</td>
           </th>
           <th>
                <td>SELECT name FROM station WHERE lat < 37.5</td>
           </th>
        </tr>
</table>

<br>

## Korea Accent

<br>

<table>
        <!-- <tr>
            <th></th>
            <th colspan="2">Ground truth</th>
            <th colspan="3">Predictions</th>
        </tr> -->
        <tr>
            <th></th>
            <th>Spoken question</th>
            <th>Text question</th>
            <th>Target SQL</th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Male Sample 1: </th>
        </tr> -->
        <tr>
            <th>Female Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK000-F-Korea/000.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>How many tracks do we have?</td>
           </th>
           <th>
                <td>SELECT count(*) FROM track</td>
           </th>
        </tr>
        <tr>
            <th>Female Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="Wav2SQL_Supplementary_Material/MASpider_audio_samples/SPK000-F-Korea/002.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <td>Show the name and location for all tracks.</td>
           </th>
           <th>
                <td>SELECT name, LOCATION FROM track</td>
           </th>
        </tr>
</table>