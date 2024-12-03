# Restro-Recommendation-TriCitiesDNG

A personalized restaurant recommendation system for New Delhi, Gurgaon, and Noida. This system uses content-based filtering combined with location-based services (LBS) and geodesic distance calculations to dynamically recommend restaurants based on user preferences and proximity.

## **Features**
- **Dynamic Recommendations**: Suggestions based on user location, preferred cuisines, and restaurant ratings.
- **Interactive Map Visualization**: View nearby restaurants and user location using Mapbox.
- **Robust Filtering**: Handles missing geolocation data using mean locality coordinates.
- **High Precision Recommendations**: Achieved 100% precision for top recommendations.

## **Technologies Used**
- Python (Pandas, Geopy, Plotly, NumPy)
- Mapbox API for geospatial visualization
- Haversine formula for geodesic distance calculations

---

## **Table of Contents**
1. [Installation](#installation)
2. [Dataset](#dataset)
3. [Methodology](#methodology)
   - [Data Preprocessing](#data-preprocessing)
   - [Recommendation Model](#recommendation-model)
   - [Geodesic Distance Calculations](#geodesic-distance-calculations)
   - [Visualization](#visualization)
4. [Results](#results)
5. [Future Enhancements](#future-enhancements)
6. [License](#license)

---

## **Installation**

1. Clone the repository:
   ```bash
   git clone https://github.com/11SST11/Restro-Recommendation-TriCitiesDNG.git
   ```
2. Navigate to the project directory:
   ```bash
   cd Restro-Recommendation-TriCitiesDNG
   ```
3. Install the required Python libraries:
   ```bash
   pip install -r requirements.txt
   ```
4. Add your Mapbox API token in the script where required.

---

## **Dataset**

The dataset was sourced from Zomato India and preprocessed to focus on three cities: New Delhi, Gurgaon, and Noida. Key attributes include:
- Restaurant Name
- Cuisine Type
- Aggregate Rating
- Votes
- Latitude/Longitude

Example Data Entry:
```json
{
  "Restaurant Name": "ABC Restaurant",
  "City": "New Delhi",
  "Locality": "Connaught Place",
  "Cuisines": "North Indian, Chinese",
  "Aggregate Rating": 4.2,
  "Votes": 150,
  "Latitude": 28.6329,
  "Longitude": 77.2195
}
```

---

## **Methodology**

### **1. Data Preprocessing**
- **Filtering**: Focused on restaurants from New Delhi, Gurgaon, and Noida.
- **Handling Missing Data**: Imputed missing latitude and longitude values using mean locality coordinates.
- **Feature Selection**: Selected attributes relevant to recommendations (e.g., cuisines, ratings, and votes).

### **2. Recommendation Model**
- **Weighted Scoring System**:
  
  The recommendation score is calculated using:
  ```math
  \text{Score} = w_1 \cdot \text{Rating Score} + w_2 \cdot \text{Distance Score} + w_3 \cdot \text{Votes Score}
  ```
  Where:
  - \( w_1, w_2, w_3 \) are weights for rating, distance, and votes respectively.
  - **Rating Score**: Normalized aggregate rating.
  - **Distance Score**: Inversely proportional to geodesic distance.
  - **Votes Score**: Normalized votes.

### **3. Geodesic Distance Calculations**
Using the Haversine formula:
```math
\text{d} = R \cdot \arccos\left(\sin(\phi_1) \cdot \sin(\phi_2) + \cos(\phi_1) \cdot \cos(\phi_2) \cdot \cos(\lambda_2 - \lambda_1)\right)
```
Where:
- \( R \): Earth’s radius (6,371 km).
- \( \phi_1, \phi_2 \): Latitudes in radians.
- \( \lambda_1, \lambda_2 \): Longitudes in radians.

### **4. Visualization**
Interactive maps were created using Plotly and Mapbox:
- **Blue Markers**: All restaurants in the dataset.
- **Red Markers**: Top recommendations.
- **Green Star**: User location.

---

## **Results**

| Metric         | Previous Approach | Enhanced Approach |
|----------------|-------------------|-------------------|
| **Precision@3** | 0.33              | -                 |
| **Recall@3**    | 0.33              | -                 |
| **Precision@5** | -                 | 1.00              |
| **Recall@5**    | -                 | 0.20              |

- **Visual Output**: Below is an example map visualization:

![Map Example](https://via.placeholder.com/600x400)

---

## **Future Enhancements**
- **Incorporate Collaborative Filtering**: To handle cold-start problems and improve recall.
- **Sentiment Analysis**: Analyze user reviews for qualitative insights into food, service, and ambiance.
- **Expand Dataset**: Include more cities to enhance scalability.
- **Hybrid Recommendation System**: Combine collaborative and content-based filtering for more comprehensive recommendations.

---

## **License**
This project is licensed under the MIT License. See the LICENSE file for more details.
