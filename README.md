# Google Timeline Parse to CSV


Parse your Google Timeline into a CSV using the following snippet. 
This is very easily done using just `jq`. 


```
jq  -r '.locations[] | (.timestampMs | tonumber | . /1000 | todate) + "," + (.latitudeE7 | tostring | .[0:2]) + "." + (.latitudeE7 | tostring | .[2:10]) + "," + (.longitudeE7 | tostring | .[0:3]) + "." + (.longitudeE7 | tostring | .[4:11])' ./Location_History.json  > locations.csv
```
**Note** If your longitude/latitude are negatives, you'll need to adjust your split numbers. 

------------------------------------------------------------

You can also filter using something like:

```
jq '.locations[] | select(.latitudeE7 <= 000000000) | select(.latitudeE7 >= 000000000) | select(.longitudeE7 <= -000000001) | select(.longitudeE7  <=  -000000001)' ./Location_History.json
```
Replace the 0's with your DD longitude/latitude. 
