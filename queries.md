https://replicator.desi.lbl.gov/TV3/app/Q/

Query A:

SELECT 
    tower_timestamp::timestamp::date || ' ' || 
    EXTRACT(HOUR FROM tower_timestamp::timestamp)::text || ':' ||
    EXTRACT(MINUTE FROM tower_timestamp::timestamp)::text || ':00' as minute_timestamp,
    MIN(gust) as gust,
    MIN(wind_direction) as wind_direction,
    MIN(wind_speed) as wind_speed
FROM environmentmonitor_tower
GROUP BY 
    tower_timestamp::timestamp::date,
    EXTRACT(HOUR FROM tower_timestamp::timestamp),
    EXTRACT(MINUTE FROM tower_timestamp::timestamp)
ORDER BY minute_timestamp DESC
