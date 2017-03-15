# weave-scope-json
Notes and tools to work with Weave Scope's JSON export

## Extract nodes with hostnames
```

    jq -r '[.Endpoint.nodes | to_entries | .[].key | capture("^(?<hostname>[a-z]{1}.*)/(?<instance>.{1}).*;.*;(?<port>.*)")] | sort | (map(keys) | add | unique) as $cols | map(. as $row | $cols | map($row[.])) as $rows | $cols, $rows[] | @csv' report.json
    
```
## References
How to convert arbirtrary simple JSON to CSV using jq?  
http://stackoverflow.com/questions/32960857/how-to-convert-arbirtrary-simple-json-to-csv-using-jq  

Ruby regular expression editor    
http://rubular.com/    
