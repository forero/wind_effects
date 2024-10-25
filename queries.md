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

Query B:

SELECT 
    row_status_time::timestamp::date || ' ' || 
    EXTRACT(HOUR FROM row_status_time::timestamp)::text || ':' ||
    EXTRACT(MINUTE FROM row_status_time::timestamp)::text || ':00' as minute_timestamp,
    AVG(mount_az) as mount_az,
    AVG(mount_el) as mount_el,
    MIN(mount_inposition) as mount_inposition,
    MIN(mount_incontrol) as mount_incontrol,
    AVG(mount_ha) as mount_ha,
    AVG(dome_az) as dome_az,
    MIN(at_zenith) as at_zenith,
    MIN(at_whitespot) as at_whitespot
FROM tcs_info
WHERE row_status_time BETWEEN '2021-01-31' AND '2024-10-23'  
GROUP BY 
    row_status_time::timestamp::date,
    EXTRACT(HOUR FROM row_status_time::timestamp),
    EXTRACT(MINUTE FROM row_status_time::timestamp)
ORDER BY minute_timestamp DESC;
