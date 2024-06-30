# BMTC Network

## **Objective**
The aim of this exercise is to identify areas within Bengaluru that are well-served or under-served by the city's road transit service, BMTC.

## **Dataset**
The data is sourced from BMTC’s GTFS (General Transit Feed Specification). For ease of data extraction, I used a script provided by geohacker, known for creating insightful map-based analyses and visualizations focused on India and its transit systems. You can find the exact source here: [BMTC GTFS](https://github.com/Vonter/bmtc-gtfs/blob/main/gtfs/bmtc.zip).

## **Scope of Analysis**

### **Defining Boundaries of Bengaluru**
The boundaries of Bengaluru are approximately within the area covered by the Peripheral Ring Road and NICE Road. This boundary is debatable, but for this exercise, it's defined by these roads. A bounding box tool using Open Street Maps was used to draw a polygon around these boundaries to obtain a set of points forming the polygon. [Bounding Box Tool](https://boundingbox.klokantech.com/).

### **Classifying Bus Stops**
Bus stops are classified based on their levels of activity:
1. **Active Stops**: ≥ 72 trips/day (a bus every 20 minutes or more frequently)
2. **Infrequent Stops**: 72 > trips/day ≥ 24 (a bus every hour to every 20 minutes)
3. **Dormant Stops**: < 24 trips/day (less than one bus every hour)

These stops will be mapped as Green, Yellow, and Red, respectively.

### **Observations on Bus Stop Activity**
Some towns and suburbs on the outskirts, like Doddaballapura, Jigani, and Bidadi, are reliably connected to the city center but not as well with each other in a circular fashion.

### **Proximity to Active Bus Stops**
Within Bengaluru's boundaries, we calculate the distance of each spot (approximated to a Geohash7, which is roughly a 150x150m area) from the nearest active bus stop. We use haversine distance rather than road walking distance for simplicity:
- **Green**: Areas within 500m of an active bus stop.
- **Yellow**: Areas between 500m to 1km.
- **Red**: Areas beyond 1km.

### **One-Stop Reachability**
We define one-stop reachability as the approximate radius of 500 meters around all stops directly and consistently reachable from a specific stop. This involves:
1. Analyzing all available direct routes originating from a designated stop.
2. Focusing on stops reachable at least 72 times daily for reliable connectivity.
3. Mapping all Geohash 8 locations (approx. 38x19m each) within a 500-meter radius of directly accessible stops from the designated point.

### **Plotting Reachability for Specific Stops**
- **Kempegowda Bus Station (Majestic)**: The nerve center of the city’s public transport infrastructure, connecting to the largest extent of Bengaluru directly.
- **Banashankari**: An old locality connected to the ring road and southern suburbs like Harohalli and Attibelle.
- **Malleshwaram**: A major cultural hub connected to the city center and northwest suburbs.
- **Tin Factory**: A junction serving as a gateway to IT corridors like ORR and Whitefield.
- **Koramangala (Water Tank)**: A startup hub fairly connected to the city center and some IT hubs but lacking connectivity to others like Bellandur and Whitefield.
- **Whitefield (ITPL)**: A major IT hub well connected to ORR and the city center by bus and metro rail.
- **Bellandur (Eco Space)**: Known for large IT parks but poorly connected to other city parts by bus.
- **Sarjapur Road (Doddakanelli)**: An emerging residential and tech hub with poor connectivity, primarily reliant on private transport.

### **Reachability Heatmap**
A heatmap, taking the log scale of reachability from designated stops, shows that the Central and Western parts of the city have relatively better direct connectivity by bus compared to the Eastern IT hubs. Improving connectivity in these IT areas could help alleviate traffic problems.
