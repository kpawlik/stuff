- [Create GeoJSON from table](#create-geojson-from-table)
- [locks](#locks)
- [blocked queries](#blocked-queries)

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

# locks
```sql
SELECT blocked_locks.pid     AS blocked_pid,
         blocked_activity.usename  AS blocked_user,
         blocking_locks.pid     AS blocking_pid,
         blocking_activity.usename AS blocking_user,
         blocked_activity.query    AS blocked_statement,
         blocking_activity.query   AS current_statement_in_blocking_process
   FROM  pg_catalog.pg_locks         blocked_locks
    JOIN pg_catalog.pg_stat_activity blocked_activity  ON blocked_activity.pid = blocked_locks.pid
    JOIN pg_catalog.pg_locks         blocking_locks 
        ON blocking_locks.locktype = blocked_locks.locktype
        AND blocking_locks.DATABASE IS NOT DISTINCT FROM blocked_locks.DATABASE
        AND blocking_locks.relation IS NOT DISTINCT FROM blocked_locks.relation
        AND blocking_locks.page IS NOT DISTINCT FROM blocked_locks.page
        AND blocking_locks.tuple IS NOT DISTINCT FROM blocked_locks.tuple
        AND blocking_locks.virtualxid IS NOT DISTINCT FROM blocked_locks.virtualxid
        AND blocking_locks.transactionid IS NOT DISTINCT FROM blocked_locks.transactionid
        AND blocking_locks.classid IS NOT DISTINCT FROM blocked_locks.classid
        AND blocking_locks.objid IS NOT DISTINCT FROM blocked_locks.objid
        AND blocking_locks.objsubid IS NOT DISTINCT FROM blocked_locks.objsubid
        AND blocking_locks.pid != blocked_locks.pid
 
    JOIN pg_catalog.pg_stat_activity blocking_activity ON blocking_activity.pid = blocking_locks.pid
   WHERE NOT blocked_locks.GRANTED;
```

# blocked queries
```sql
SELECT
  COALESCE(blockingl.relation::regclass::text,blockingl.locktype) as locked_item,
  now() - blockeda.query_start AS waiting_duration, blockeda.pid AS blocked_pid,
  blockeda.query as blocked_query, blockedl.mode as blocked_mode,
  blockinga.pid AS blocking_pid, blockinga.query as blocking_query,
  blockingl.mode as blocking_mode
FROM pg_catalog.pg_locks blockedl
JOIN pg_stat_activity blockeda ON blockedl.pid = blockeda.pid
JOIN pg_catalog.pg_locks blockingl ON(
  ( (blockingl.transactionid=blockedl.transactionid) OR
  (blockingl.relation=blockedl.relation AND blockingl.locktype=blockedl.locktype)
  ) AND blockedl.pid != blockingl.pid)
JOIN pg_stat_activity blockinga ON blockingl.pid = blockinga.pid
  AND blockinga.datid = blockeda.datid
WHERE NOT blockedl.granted
AND blockinga.datname = 'mw';
```
