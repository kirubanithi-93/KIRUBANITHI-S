
| Field Name          | Data Type    | Description                          | Example Value          | Source               |
|---------------------|--------------|--------------------------------------|------------------------|----------------------|
| `observation_id`    | UUID         | Unique record identifier             | "a1b2-c3d4-e5f6..."    | System-generated    |
| `timestamp`         | DateTime     | Time of data collection              | "2025-05-19 08:15:00"  | IoT Sensors         |
| `road_segment_id`   | ForeignKey   | Linked to Road_Segments table        | "RS-2056"              | GIS Database        |
| `speed_avg`         | Float (km/h) | Average vehicle speed                | 62.4                   | Radar/LIDAR         |
| `vehicle_count`     | Integer      | Vehicles detected in 5-min window    | 148                    | Loop Detectors      |
| `occupancy_rate`    | Float (%)    | Road space utilization               | 78.2                   | Camera AI           |
| `vehicle_types`     | JSON         | Classification (cars, trucks, etc.)  | `{"car":120, "truck":28}` | Computer Vision  |
| `weather_id`        | ForeignKey   | Linked to Weather_Conditions table   | "WX-20250519-0815"     | Weather API         |
| `road_name`       | String       | Street/highway name                 | "I-95 Northbound"         |
| `start_coord`     | GeoPoint     | Latitude/Longitude (start)          | "39.1234, -77.5432".      |
| `end_coord`       | GeoPoint     | Latitude/Longitude (end)            | "39.1256, -77.5401".      |
| `length_km`       | Float        | Segment length in kilometers        | 0.75                      |
| `lanes`           | Integer      | Number of lanes                     | 4                         |
| `speed_limit`     | Integer      | Legal speed limit (km/h)            | 100                       |
| `road_condition`  | Enum         | [Paved/Unpaved/Construction]       | "Paved"                    |
| `weather_id`     | String       | Timestamp + location hash           | "WX-20250519-0815"         |
| `timestamp`      | DateTime     | Time of weather data                | "2025-05-19 08:15:00" |
| `temperature`    | Float (°C)   | Ambient temperature                 | 22.5                  |
| `precipitation`  | Float (mm/h) | Rainfall intensity                  | 0.0                   |
| `visibility`     | Integer (m)  | Visibility range                    | 10000                 |
| `road_surface`   | Enum         | [Dry/Wet/Snowy/Icy]                | "Dry"                 |
| `traffic_patterns`       | Hourly/daily traffic trends         | Speed/volume baselines               |
| `congestion_hotspots`    | Recurrent bottleneck analysis       | Delay duration, frequency            |
| `od_matrix`             | Origin-Destination flow modeling    | Trip routes, peak demand times       |
| `predictive_alerts`      | AI-generated incident forecasts     | Probability scores (0-100%)   
|## **Accident Analysis Datasets Tabulation**

| **Category**               | **Dataset Name**               | **Key Fields**                                                                 | **Data Source**                | **Update Frequency** | **AI Use Case**                                  | **Accident Analysis Value**                                                                 |
|----------------------------|--------------------------------|-------------------------------------------------------------------------------|--------------------------------|----------------------|--------------------------------------------------|---------------------------------------------------------------------------------------------|
| **1. Core Accident Data**                                                                                                                                                                 |
| 1.1                        | Police Crash Reports           | crash_id, location, severity, collision_type, weather, road_condition        | Law Enforcement               | Event-based          | Pattern recognition                             | Identifies high-risk locations and collision types (e.g., rear-end vs. T-bone)              |
| 1.2                        | Emergency Response Logs        | response_time, injury_severity, fatalities, responder_type                   | EMS/Fire Departments          | Event-based          | Resource allocation                             | Correlates response times with outcomes (e.g., fatality reduction)                          |
| 1.3                        | Traffic Camera Footage         | timestamp, camera_id, pre/post_crash_video, vehicle_actions                  | CCTV Networks                 | Real-time            | Computer vision analysis                        | Reveals driver behavior (e.g., sudden braking, swerving) before crashes                     |
| 1.4                        | Crowdsourced Incident Reports  | user_id, report_time, crash_type, confidence_score                           | Waze/Google Maps              | 1 min                | Real-time alerts                                | Validates official reports and provides faster incident detection                           |
| 1.5                        | Insurance Claims               | claim_id, damage_cost, injury_details, liability                             | Insurance Companies           | Daily                | Fraud detection                                 | Quantifies financial impact and common claim patterns                                       |

| **2. Contextual & Environmental Data**                                                                                                                                                    |
| 2.1                        | Road Geometry & Design         | segment_id, curvature, grade, sight_distance, guardrail_presence             | GIS/DOT Databases             | Static               | Infrastructure risk scoring                     | Flags design flaws (e.g., sharp curves with poor visibility)                                |
| 2.2                        | Weather at Time of Crash       | temp, precipitation, visibility, wind_speed                                  | NOAA/RWIS                     | Event-based          | Conditional risk modeling                       | Links weather to crash likelihood (e.g., icy roads → 3× higher rear-end crashes)            |
| 2.3                        | Traffic Volume & Speed         | segment_id, avg_speed, volume, congestion_level                              | Loop Detectors                | 5 min                | Density-risk correlation                        | Shows if crashes spike during high-volume or low-speed conditions                           |
| 2.4                        | Work Zone Activity             | location, duration, lane_closures, signage                                   | DOT Feeds                     | Daily                | Construction zone safety                        | Evaluates crash rates near work zones (e.g., 40% increase in sideswipes)                    |
| 2.5                        | Lighting Conditions            | light_level (day/night/dusk), streetlight_status                             | Smart City Sensors            | 15 min               | Nighttime accident prevention                   | Quantifies crash risk in low-light areas (e.g., 2.5× more pedestrian accidents at night)     |

| **3. Vehicle & Driver Factors**                                                                                                                                                          |
| 3.1                        | Vehicle Telematics             | speed, braking_force, steering_angle, ABS_activation                         | Event Data Recorders (EDRs)   | Event-based          | Driver behavior analysis                        | Proves speeding/aggressive driving in 78% of severe crashes                                 |
| 3.2                        | Driver History                 | license_id, prior_offenses, DUI_records                                      | DMV                           | Monthly              | Risk profiling                                  | Flags high-risk drivers (e.g., DUI history → 5× crash risk)                                 |
| 3.3                        | Vehicle Defects                | VIN, recall_status, tire_condition, brake_wear                               | NHTSA Databases               | Weekly               | Mechanical failure attribution                  | Links defects to crash causes (e.g., tire blowouts in 12% of run-off-road crashes)          |
| 3.4                        | Ride-Hailing Driver Metrics    | trip_id, harsh_events, distraction_alerts                                    | Uber/Lyft                     | Daily                | Fleet safety benchmarking                       | Compares professional vs. private driver crash rates                                        |

| **4. Derived Analytics**                                                                                                                                                                |
| 4.1                        | Accident Hotspots              | location, crash_frequency, severity_index                                    | Spatial clustering            | Monthly              | Targeted enforcement                            | Identifies top 5% of locations causing 20% of crashes                                       |
| 4.2                        | Severity Prediction Model      | features: speed, impact_angle, restraint_use → outcome: injury_level        | Machine learning             | Real-time            | EMS prioritization                              | Predicts 92% accuracy in classifying fatal vs. non-fatal crashes                            |
| 4.3                        | Time-to-Clearance Analysis     | crash_time, lane_closure_duration, traffic_impact                            | Historical logs              | Event-based          | Traffic management                              | Reduces secondary crashes by 30% with faster clearance                                      |
| 4.4                        | Economic Impact Calculator     | medical_costs, property_damage, congestion_costs                            | Insurance + DOT data         | Annual               | Cost-benefit analysis                           | Shows $1M investment in guardrails prevents $4.2M in annual crash costs                     |

| **5. Emerging Data Sources**                                                                                                                                                            |
| 5.1                        | Social Media Sentiment         | keyword: "crash", location, panic_level                                      | Twitter/Reddit               | 1 min                | Early detection                                 | Detects 15% of crashes before official reports                                              |
| 5.2                        | Autonomous Vehicle Near-Misses | AV_id, avoidance_maneuver, object_type
