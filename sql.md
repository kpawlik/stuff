# Create GeoJSON from table 
```sql
psql -c "\COPY (SELECT jsonb_build_object(
    'type',     'FeatureCollection',
    'features', jsonb_agg(features.feature)
)
FROM (
  SELECT jsonb_build_object(
    'type',       'Feature',
    'id',         id,
    'geometry',   ST_AsGeoJSON(the_geom)::jsonb,
    'properties', to_jsonb(inputs) - 'id' - 'name'
  ) AS feature
  FROM (SELECT id,name,the_geom FROM data.amplifier where the_geom is not null limit 10) inputs) features) TO /tmp/test.json;
"
```
