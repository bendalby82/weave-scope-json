# weave-scope-json
Notes and tools to work with Weave Scope's JSON export

## Extract nodes with hostnames  
```
jq -r '[.Endpoint.nodes | to_entries | .[].key | capture("^(?<hostname>[a-z]{1}.*)/(?<instance>.{1}).*;.*;(?<port>.*)")] | sort | (map(keys) | add | unique) as $cols | map(. as $row | $cols | map($row[.])) as $rows | $cols, $rows[] | @csv' report.json
    
```
## Extract hosts and adjacent hosts, splitting hostname, IP and port  
```
jq -r '["Host Name","Host IP","Host Port","Remote Host","Remote IP","Remote Port"],(.Endpoint.nodes | to_entries | .[] | [.key,.value.adjacency[0] // ";;"] | map (split(";")) | flatten) | @csv' report.json
```
## References
How to convert arbirtrary simple JSON to CSV using jq?  
http://stackoverflow.com/questions/32960857/how-to-convert-arbirtrary-simple-json-to-csv-using-jq  

Split multiple property values in JSON object array with jq  
http://stackoverflow.com/questions/42930707/split-multiple-property-values-in-json-object-array-with-jq

Ruby regular expression editor    
http://rubular.com/    

JQ Play  
https://jqplay.org/  

tsv and/or csv output support  
https://github.com/stedolan/jq/issues/48  
