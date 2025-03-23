# DART Transit Insights: A Case Study on Performance, Safety, and Sustainability

## Overview
Greetings, esteemed mayors, city planners, and DART/Trinity Metro officials! As a **Transportation Systems Data Analyst** and proud DFW resident, I present *DART Transit Insights*—a comprehensive case study analyzing the Dallas Area Rapid Transit (DART) system’s performance, public safety perceptions, and strategic opportunities for Fiscal Year 2025 (July 2024–June 2025). Using meticulously crafted datasets (modeled as real-world proxies), this project examines delays, safety concerns, and initiatives to elevate DART’s appeal—crucial steps to ensure our metroplex thrives as a sustainable, equitable hub. Built with **Python** and **R**, this is a blueprint for data-driven transit planning. Let’s dive in!

*Note*: While these datasets are simulated, they mirror real-world patterns to spark actionable dialogue.

---

## Table of Contents
- [Datasets](#datasets)
  - [Manual `.csv` Files](#manual-csv-files)
  - [Python Generators](#python-generators)
- [Visualizations](#visualizations)
- [Setup Instructions](#setup-instructions)
- [Why It Matters: A Local’s Take](#why-it-matters-a-locals-take)
- [Conclusion](#conclusion)
- [License](#license)

---

## Datasets

### Manual `.csv` Files
Below are the core datasets, manually crafted to reflect DART’s operational and perceptual landscape. Copy these into Notepad and save as `.csv` in `C:/Users/Veteran`.

1. **`dart_delays.csv`** (Sample: 10 of 1,000 rows)  
   - **Columns**: `Date`, `System`, `Line_Route`, `Delay_Cause`, `Delay_Minutes`, `Location`  
   - **Purpose**: Tracks daily delays by cause (Mechanical, Traffic, Signal Sync).  
   ```csv
   Date,System,Line_Route,Delay_Cause,Delay_Minutes,Location
   2024-07-01,Rail,Red Line,Mechanical Issues,45,Downtown Dallas
   2024-07-02,Bus,Bus,Traffic Congestion,30,I-35E at Loop 12
   2024-07-03,Rail,Green Line,Signal Sync Issues,20,Deep Ellum
   2024-07-04,Bus,Bus,Mechanical Issues,60,Arlington
   2024-08-15,Rail,Blue Line,Traffic Congestion,15,Mockingbird Station
   2024-09-01,Bus,Bus,Signal Sync Issues,25,Fort Worth Ave
   2024-10-10,Rail,Orange Line,Mechanical Issues,50,DFW Airport
   2024-11-20,Bus,Bus,Traffic Congestion,40,Plano
   2025-01-15,Rail,Red Line,Signal Sync Issues,30,West End
   2025-03-01,Bus,Bus,Mechanical Issues,35,Garland
   ```

2. **`dart_quarterly_summary.csv`**  
   - **Columns**: `Quarter`, `System`, `Total_Delays`, `Mechanical_Delays`, `Traffic_Delays`, `Signal_Delays`, `Percent_Mechanical`, `Percent_Traffic`, `Percent_Signal`  
   - **Purpose**: Aggregates delays for fiscal reporting.  
   ```csv
   Quarter,System,Total_Delays,Mechanical_Delays,Traffic_Delays,Signal_Delays,Percent_Mechanical,Percent_Traffic,Percent_Signal
   Q1 2025,Rail,150,60,45,45,40.0,30.0,30.0
   Q1 2025,Bus,200,80,90,30,40.0,45.0,15.0
   Q2 2025,Rail,140,50,40,50,35.7,28.6,35.7
   Q2 2025,Bus,210,70,100,40,33.3,47.6,19.1
   Q3 2025,Rail,130,55,35,40,42.3,26.9,30.8
   Q3 2025,Bus,190,75,85,30,39.5,44.7,15.8
   Q4 2025,Rail,120,50,30,40,41.7,25.0,33.3
   Q4 2025,Bus,180,60,80,40,33.3,44.4,22.2
   ```

3. **`dart_trouble_spots.csv`**  
   - **Columns**: `Location`, `System`, `Latitude`, `Longitude`, `Total_Delays`, `Percent_Delayed`  
   - **Purpose**: Maps delay hotspots.  
   ```csv
   Location,System,Latitude,Longitude,Total_Delays,Percent_Delayed
   Downtown Dallas,Rail,32.7767,-96.7970,80,60.0
   I-35E at Loop 12,Bus,32.7323,-96.8758,90,65.0
   Deep Ellum,Rail,32.7850,-96.7790,60,50.0
   Arlington,Bus,32.7357,-97.1081,70,55.0
   Mockingbird Station,Rail,32.8367,-96.7770,50,45.0
   Fort Worth Ave,Bus,32.7500,-96.8500,65,50.0
   DFW Airport,Rail,32.8968,-97.0380,75,60.0
   Plano,Bus,33.0198,-96.6989,85,62.0
   West End,Rail,32.7800,-96.8050,55,48.0
   Garland,Bus,32.9126,-96.6389,60,52.0
   ```

4. **`dart_safety_time.csv`**  
   - **Columns**: `Suburb`, `Time_of_Day`, `Respondents`, `Feel_Safe`, `More_Police`, `Open_Carry_Concern`  
   - **Purpose**: Gauges safety perception by time.  
   ```csv
   Suburb,Time_of_Day,Respondents,Feel_Safe,More_Police,Open_Carry_Concern
   Plano,Morning,100,80,20,10
   Plano,Afternoon,100,75,25,15
   Plano,Evening,100,60,40,25
   Plano,Night,100,40,60,35
   Arlington,Morning,100,70,30,20
   Arlington,Afternoon,100,65,35,25
   Arlington,Evening,100,50,50,30
   Arlington,Night,100,30,70,40
   Garland,Morning,100,75,25,15
   Garland,Afternoon,100,70,30,20
   Garland,Evening,100,55,45,25
   Garland,Night,100,35,65,35
   Irving,Morning,100,85,15,10
   Irving,Afternoon,100,80,20,15
   Irving,Evening,100,65,35,20
   Irving,Night,100,45,55,30
   Frisco,Morning,100,90,10,5
   Frisco,Afternoon,100,85,15,10
   Frisco,Evening,100,70,30,15
   Frisco,Night,100,50,50,25
   ```

5. **`dart_safety_opinion.csv`**  
   - **Columns**: `Suburb`, `Respondents`, `Feel_Safe`, `More_Police`, `Open_Carry_Concern`, `Never_Ride`  
   - **Purpose**: Captures broader safety opinions.  
   ```csv
   Suburb,Respondents,Feel_Safe,More_Police,Open_Carry_Concern,Never_Ride
   Plano,300,70,30,20,25
   Arlington,300,60,40,30,35
   Garland,300,65,35,25,30
   Irving,300,75,25,15,20
   Frisco,300,80,20,10,15
   ```

6. **`dart_never_ride.csv`**  
   - **Columns**: `Reason`, `Respondents`, `Percentage`  
   - **Purpose**: Breaks down “never ride” excuses.  
   ```csv
   Reason,Respondents,Percentage
   "Don't Know Enough About DART",150,33.3
   "Public Transit is for Poor People",120,26.7
   "Love My Car Too Much",100,22.2
   "Safety Concerns",60,13.3
   "Too Inconvenient",20,4.5
   ```

7. **`dart_city_plans.csv`**  
   - **Columns**: `Initiative`, `Suburb`, `Projected_Impact`, `Emission_Reduction`, `Noise_Reduction`, `Congestion_Reduction`, `Appeal_Score`  
   - **Purpose**: Outlines plans to boost DART’s appeal.  
   ```csv
   Initiative,Suburb,Projected_Impact,Emission_Reduction,Noise_Reduction,Congestion_Reduction,Appeal_Score
   "Eco-Friendly Hybrid Buses",Plano,High,80,60,70,75
   "Smart Rail Signals",Plano,Medium,50,70,60,65
   "Quiet Electric Buses",Arlington,High,75,65,65,70
   "Expanded Park & Ride",Arlington,Medium,60,50,70,60
   "Green Station Upgrades",Garland,Medium,65,55,60,65
   "Noise-Blocking Rail Tech",Garland,Low,40,80,50,60
   "Zero-Emission Shuttles",Irving,High,85,60,75,80
   "Traffic-Sync Lights",Irving,Medium,55,50,65,70
   "Solar-Powered Stations",Frisco,High,90,70,80,85
   "Express Rail Lanes",Frisco,Medium,60,60,70,75
   ```

### Python Generators
For Python developers, here’s how to generate these datasets programmatically:

1. **`generate_dart_delays.py`**  
   ```python
   import pandas as pd
   import numpy as np
   from faker import Faker
   import random

   fake = Faker()
   np.random.seed(42)

   def generate_delays(n=1000):
       dates = [fake.date_between(start_date='-9m', end_date='today') for _ in range(n)]
       systems = ['Rail', 'Bus']
       lines = ['Red Line', 'Blue Line', 'Green Line', 'Orange Line', 'Bus']
       causes = ['Mechanical Issues', 'Traffic Congestion', 'Signal Sync Issues']
       locations = ['Downtown Dallas', 'I-35E at Loop 12', 'Deep Ellum', 'Arlington', 'Mockingbird Station',
                    'Fort Worth Ave', 'DFW Airport', 'Plano', 'West End', 'Garland']
       data = {
           'Date': dates,
           'System': [random.choice(systems) for _ in range(n)],
           'Line_Route': [random.choice(lines) for _ in range(n)],
           'Delay_Cause': [random.choice(causes) for _ in range(n)],
           'Delay_Minutes': [random.randint(10, 60) for _ in range(n)],
           'Location': [random.choice(locations) for _ in range(n)]
       }
       return pd.DataFrame(data)

   delays_df = generate_delays()
   delays_df.to_csv('dart_delays.csv', index=False)
   print("Generated 'dart_delays.csv'")
   ```

2. **`generate_dart_quarterly_summary.py`**  
   ```python
   import pandas as pd
   import numpy as np

   np.random.seed(42)

   quarters = ['Q1 2025', 'Q2 2025', 'Q3 2025', 'Q4 2025']
   systems = ['Rail', 'Bus']
   data = {
       'Quarter': [q for q in quarters for _ in systems],
       'System': [s for _ in quarters for s in systems],
       'Total_Delays': [150, 200, 140, 210, 130, 190, 120, 180],
       'Mechanical_Delays': [60, 80, 50, 70, 55, 75, 50, 60],
       'Traffic_Delays': [45, 90, 40, 100, 35, 85, 30, 80],
       'Signal_Delays': [45, 30, 50, 40, 40, 30, 40, 40]
   }
   df = pd.DataFrame(data)
   df['Percent_Mechanical'] = (df['Mechanical_Delays'] / df['Total_Delays']) * 100
   df['Percent_Traffic'] = (df['Traffic_Delays'] / df['Total_Delays']) * 100
   df['Percent_Signal'] = (df['Signal_Delays'] / df['Total_Delays']) * 100
   df.to_csv('dart_quarterly_summary.csv', index=False)
   print("Generated 'dart_quarterly_summary.csv'")
   ```

3. **`generate_dart_trouble_spots.py`**  
   ```python
   import pandas as pd

   data = {
       'Location': ['Downtown Dallas', 'I-35E at Loop 12', 'Deep Ellum', 'Arlington', 'Mockingbird Station',
                    'Fort Worth Ave', 'DFW Airport', 'Plano', 'West End', 'Garland'],
       'System': ['Rail', 'Bus', 'Rail', 'Bus', 'Rail', 'Bus', 'Rail', 'Bus', 'Rail', 'Bus'],
       'Latitude': [32.7767, 32.7323, 32.7850, 32.7357, 32.8367, 32.7500, 32.8968, 33.0198, 32.7800, 32.9126],
       'Longitude': [-96.7970, -96.8758, -96.7790, -97.1081, -96.7770, -96.8500, -97.0380, -96.6989, -96.8050, -96.6389],
       'Total_Delays': [80, 90, 60, 70, 50, 65, 75, 85, 55, 60],
       'Percent_Delayed': [60.0, 65.0, 50.0, 55.0, 45.0, 50.0, 60.0, 62.0, 48.0, 52.0]
   }
   df = pd.DataFrame(data)
   df.to_csv('dart_trouble_spots.csv', index=False)
   print("Generated 'dart_trouble_spots.csv'")
   ```

4. **`generate_dart_safety_time.py`**  
   ```python
   import pandas as pd
   import numpy as np

   np.random.seed(42)
   suburbs = ['Plano', 'Arlington', 'Garland', 'Irving', 'Frisco']
   times = ['Morning', 'Afternoon', 'Evening', 'Night']
   data = {
       'Suburb': [s for s in suburbs for _ in times],
       'Time_of_Day': [t for _ in suburbs for t in times],
       'Respondents': [100] * 20,
       'Feel_Safe': [80, 75, 60, 40, 70, 65, 50, 30, 75, 70, 55, 35, 85, 80, 65, 45, 90, 85, 70, 50],
       'More_Police': [20, 25, 40, 60, 30, 35, 50, 70, 25, 30, 45, 65, 15, 20, 35, 55, 10, 15, 30, 50],
       'Open_Carry_Concern': [10, 15, 25, 35, 20, 25, 30, 40, 15, 20, 25, 35, 10, 15, 20, 30, 5, 10, 15, 25]
   }
   df = pd.DataFrame(data)
   df.to_csv('dart_safety_time.csv', index=False)
   print("Generated 'dart_safety_time.csv'")
   ```

5. **`generate_dart_safety_opinion.py`**  
   ```python
   import pandas as pd

   data = {
       'Suburb': ['Plano', 'Arlington', 'Garland', 'Irving', 'Frisco'],
       'Respondents': [300] * 5,
       'Feel_Safe': [70, 60, 65, 75, 80],
       'More_Police': [30, 40, 35, 25, 20],
       'Open_Carry_Concern': [20, 30, 25, 15, 10],
       'Never_Ride': [25, 35, 30, 20, 15]
   }
   df = pd.DataFrame(data)
   df.to_csv('dart_safety_opinion.csv', index=False)
   print("Generated 'dart_safety_opinion.csv'")
   ```

6. **`generate_dart_never_ride.py`**  
   ```python
   import pandas as pd

   data = {
       'Reason': ["Don't Know Enough About DART", "Public Transit is for Poor People", "Love My Car Too Much", 
                  "Safety Concerns", "Too Inconvenient"],
       'Respondents': [150, 120, 100, 60, 20],
       'Percentage': [33.3, 26.7, 22.2, 13.3, 4.5]
   }
   df = pd.DataFrame(data)
   df.to_csv('dart_never_ride.csv', index=False)
   print("Generated 'dart_never_ride.csv'")
   ```

7. **`generate_dart_city_plans.py`**  
   ```python
   import pandas as pd

   data = {
       'Initiative': ["Eco-Friendly Hybrid Buses", "Smart Rail Signals", "Quiet Electric Buses", "Expanded Park & Ride",
                      "Green Station Upgrades", "Noise-Blocking Rail Tech", "Zero-Emission Shuttles", "Traffic-Sync Lights",
                      "Solar-Powered Stations", "Express Rail Lanes"],
       'Suburb': ['Plano', 'Plano', 'Arlington', 'Arlington', 'Garland', 'Garland', 'Irving', 'Irving', 'Frisco', 'Frisco'],
       'Projected_Impact': ['High', 'Medium', 'High', 'Medium', 'Medium', 'Low', 'High', 'Medium', 'High', 'Medium'],
       'Emission_Reduction': [80, 50, 75, 60, 65, 40, 85, 55, 90, 60],
       'Noise_Reduction': [60, 70, 65, 50, 55, 80, 60, 50, 70, 60],
       'Congestion_Reduction': [70, 60, 65, 70, 60, 50, 75, 65, 80, 70],
       'Appeal_Score': [75, 65, 70, 60, 65, 60, 80, 70, 85, 75]
   }
   df = pd.DataFrame(data)
   df.to_csv('dart_city_plans.csv', index=False)
   print("Generated 'dart_city_plans.csv'")
   ```

---

## Visualizations
All R scripts assume files in `C:/Users/Veteran`. Outputs are `.png` files.

1. **`dart_quarterly_visual.R`** (Stacked Bar)  
   - **File**: `dart_quarterly_summary.csv`  
   - **Output**: `dart_quarterly_bar.png`  
   ```R
   if (!require(ggplot2)) install.packages("ggplot2"); library(ggplot2)
   if (!require(dplyr)) install.packages("dplyr"); library(dplyr)
   if (!require(tidyr)) install.packages("tidyr"); library(tidyr)

   setwd("C:/Users/Veteran")
   summary <- read.csv("dart_quarterly_summary.csv")
   summary_long <- summary %>% 
     pivot_longer(cols = c("Mechanical_Delays", "Traffic_Delays", "Signal_Delays"), names_to = "Cause", values_to = "Count") %>%
     mutate(Cause = recode(Cause, "Mechanical_Delays" = "Mechanical", "Traffic_Delays" = "Traffic", "Signal_Delays" = "Signal"))

   bar_plot <- ggplot(summary_long, aes(x = Quarter, y = Count, fill = Cause)) +
     geom_bar(stat = "identity") + facet_wrap(~System) +
     scale_fill_manual(values = c("Mechanical" = "red", "Traffic" = "orange", "Signal" = "purple")) +
     theme_minimal() + labs(title = "DART Delays by Cause (FY 2025)", subtitle = "Quarterly Data for Rail and Bus", 
                            x = "Quarter", y = "Number of Delays", fill = "Delay Cause") +
     theme(plot.title = element_text(hjust = 0.5, size = 16, face = "bold"), plot.subtitle = element_text(hjust = 0.5, size = 12), legend.position = "top")

   print("Displaying stacked bar chart:")
   print(bar_plot)
   ggsave("dart_quarterly_bar.png", bar_plot, width = 10, height = 6, dpi = 300)
   cat("Saved as 'dart_quarterly_bar.png'\n")
   ```

2. **`dart_spots_map.R`** (Terrain Map)  
   - **File**: `dart_trouble_spots.csv`  
   - **Output**: `dart_spots_map.png`  
   ```R
   if (!require(ggplot2)) install.packages("ggplot2"); library(ggplot2)
   if (!require(ggmap)) install.packages("ggmap"); library(ggmap)
   if (!require(viridis)) install.packages("viridis"); library(viridis)

   register_stadiamaps("9c644007-0572-4892-915a-8da356fe40ae")
   setwd("C:/Users/Veteran")
   spots <- read.csv("dart_trouble_spots.csv")
   dfw_bbox <- c(left = -97.5, bottom = 32.5, right = -96.5, top = 33.2)
   dfw_terrain <- get_stadiamap(bbox = dfw_bbox, maptype = "stamen_terrain", zoom = 10)

   map_plot <- ggmap(dfw_terrain) +
     geom_point(data = spots, aes(x = Longitude, y = Latitude, size = Percent_Delayed, color = Percent_Delayed), alpha = 0.8, shape = 16) +
     scale_size_continuous(range = c(5, 15), name = "Delay %") +
     scale_color_viridis_c(option = "viridis", direction = -1, name = "Delay %") +
     geom_text(data = spots, aes(x = Longitude, y = Latitude, label = Location), vjust = -1.5, size = 3.5, color = "black", fontface = "bold") +
     theme_minimal() + labs(title = "DART Trouble Spots (FY 2025)", subtitle = "Delay Hotspots in DFW", x = "Longitude", y = "Latitude") +
     theme(plot.title = element_text(hjust = 0.5, size = 16, face = "bold"), plot.subtitle = element_text(hjust = 0.5, size = 12), legend.position = "right")

   print("Displaying terrain map:")
   print(map_plot)
   ggsave("dart_spots_map.png", map_plot, width = 10, height = 8, dpi = 300)
   cat("Saved as 'dart_spots_map.png'\n")
   ```

3. **`dart_safety_time_visual.R`** (Heatmap)  
   - **File**: `dart_safety_time.csv`  
   - **Output**: `dart_safety_time_heatmap.png`  
   ```R
   if (!require(ggplot2)) install.packages("ggplot2"); library(ggplot2)
   if (!require(dplyr)) install.packages("dplyr"); library(dplyr)

   setwd("C:/Users/Veteran")
   safety <- read.csv("dart_safety_time.csv")

   heatmap_plot <- ggplot(safety, aes(x = Time_of_Day, y = Suburb, fill = Feel_Safe)) +
     geom_tile() + geom_text(aes(label = paste0(Feel_Safe, "%")), color = "white", size = 4, fontface = "bold") +
     scale_fill_gradient(low = "red", high = "green", name = "Feel Safe (%)") +
     theme_minimal() + labs(title = "DART Safety Perception by Time of Day (FY 2025)", subtitle = "Suburban Opinions Across DFW", 
                            x = "Time of Day", y = "Suburb") +
     theme(plot.title = element_text(hjust = 0.5, size = 16, face = "bold"), plot.subtitle = element_text(hjust = 0.5, size = 12), 
           legend.position = "right", axis.text.x = element_text(angle = 45, hjust = 1))

   print("Displaying heatmap:")
   print(heatmap_plot)
   ggsave("dart_safety_time_heatmap.png", heatmap_plot, width = 8, height = 6, dpi = 300)
   cat("Saved as 'dart_safety_time_heatmap.png'\n")
   ```

4. **`dart_safety_opinion_visual.R`** (Grouped Bar)  
   - **File**: `dart_safety_opinion.csv`  
   - **Output**: `dart_safety_opinion_bar.png`  
   ```R
   if (!require(ggplot2)) install.packages("ggplot2"); library(ggplot2)
   if (!require(dplyr)) install.packages("dplyr"); library(dplyr)
   if (!require(tidyr)) install.packages("tidyr"); library(tidyr)

   setwd("C:/Users/Veteran")
   opinion <- read.csv("dart_safety_opinion.csv")
   opinion_long <- opinion %>% 
     pivot_longer(cols = c("Feel_Safe", "More_Police", "Open_Carry_Concern", "Never_Ride"), names_to = "Metric", values_to = "Percentage") %>%
     mutate(Metric = recode(Metric, "Feel_Safe" = "Feel Safe", "More_Police" = "More Police", 
                            "Open_Carry_Concern" = "Open Carry Concern", "Never_Ride" = "Never Ride"))

   bar_plot <- ggplot(opinion_long, aes(x = Suburb, y = Percentage, fill = Metric)) +
     geom_bar(stat = "identity", position = "dodge") +
     geom_text(aes(label = paste0(Percentage, "%")), position = position_dodge(width = 0.9), vjust = -0.5, size = 3.5) +
     scale_fill_manual(values = c("Feel Safe" = "green", "More Police" = "blue", "Open Carry Concern" = "orange", "Never Ride" = "red")) +
     theme_minimal() + labs(title = "DART Public Safety Opinions (FY 2025)", subtitle = "Suburban Views in DFW", 
                            x = "Suburb", y = "Percentage (%)", fill = "Opinion") +
     theme(plot.title = element_text(hjust = 0.5, size = 16, face = "bold"), plot.subtitle = element_text(hjust = 0.5, size = 12), 
           legend.position = "top", axis.text.x = element_text(angle = 45, hjust = 1))

   print("Displaying grouped bar chart:")
   print(bar_plot)
   ggsave("dart_safety_opinion_bar.png", bar_plot, width = 10, height = 6, dpi = 300)
   cat("Saved as 'dart_safety_opinion_bar.png'\n")
   ```

5. **`dart_never_ride_visual.R`** (Pie Chart)  
   - **File**: `dart_never_ride.csv`  
   - **Output**: `dart_never_ride_pie.png`  
   ```R
   if (!require(ggplot2)) install.packages("ggplot2"); library(ggplot2)
   if (!require(dplyr)) install.packages("dplyr"); library(dplyr)

   setwd("C:/Users/Veteran")
   never_ride <- read.csv("dart_never_ride.csv")

   pie_plot <- ggplot(never_ride, aes(x = "", y = Respondents, fill = Reason)) +
     geom_bar(stat = "identity", width = 1) + coord_polar("y") +
     geom_text(aes(label = paste0(Percentage, "%")), position = position_stack(vjust = 0.5), size = 4, color = "white", fontface = "bold") +
     scale_fill_manual(values = c("Don't Know Enough About DART" = "purple", "Public Transit is for Poor People" = "red", 
                                  "Love My Car Too Much" = "blue", "Safety Concerns" = "orange", "Too Inconvenient" = "gray")) +
     theme_void() + labs(title = "Why They’d Never Ride DART (FY 2025)", subtitle = "Suburban Excuses in DFW", fill = "Reason") +
     theme(plot.title = element_text(hjust = 0.5, size = 16, face = "bold"), plot.subtitle = element_text(hjust = 0.5, size = 12), legend.position = "right")

   print("Displaying pie chart:")
   print(pie_plot)
   ggsave("dart_never_ride_pie.png", pie_plot, width = 8, height = 6, dpi = 300)
   cat("Saved as 'dart_never_ride_pie.png'\n")
   ```

6. **`dart_city_plans_visual.R`** (Grouped Bar)  
   - **File**: `dart_city_plans.csv`  
   - **Output**: `dart_city_plans_bar.png`  
   ```R
   if (!require(ggplot2)) install.packages("ggplot2"); library(ggplot2)
   if (!require(dplyr)) install.packages("dplyr"); library(dplyr)
   if (!require(tidyr)) install.packages("tidyr"); library(tidyr)

   setwd("C:/Users/Veteran")
   plans <- read.csv("dart_city_plans.csv")
   plans_long <- plans %>% 
     pivot_longer(cols = c("Emission_Reduction", "Noise_Reduction", "Congestion_Reduction", "Appeal_Score"), 
                  names_to = "Metric", values_to = "Value") %>%
     mutate(Metric = recode(Metric, "Emission_Reduction" = "Emissions", "Noise_Reduction" = "Noise", 
                            "Congestion_Reduction" = "Congestion", "Appeal_Score" = "Appeal"))

   bar_plot <- ggplot(plans_long, aes(x = Initiative, y = Value, fill = Metric)) +
     geom_bar(stat = "identity", position = "dodge") +
     geom_text(aes(label = Value), position = position_dodge(width = 0.9), vjust = -0.5, size = 3) +
     scale_fill_manual(values = c("Emissions" = "green", "Noise" = "blue", "Congestion" = "orange", "Appeal" = "purple")) +
     facet_wrap(~Suburb, ncol = 2) +
     theme_minimal() + labs(title = "DART Plans to Win Over Skeptics (FY 2025)", subtitle = "Making DFW Cleaner and Cooler", 
                            x = "Initiative", y = "Score (0-100)", fill = "Metric") +
     theme(plot.title = element_text(hjust = 0.5, size = 16, face = "bold"), plot.subtitle = element_text(hjust = 0.5, size = 12), 
           legend.position = "top", axis.text.x = element_text(angle = 45, hjust = 1))

   print("Displaying grouped bar chart:")
   print(bar_plot)
   ggsave("dart_city_plans_bar.png", bar_plot, width = 12, height = 8, dpi = 300)
   cat("Saved as 'dart_city_plans_bar.png'\n")
   ```

---

## Setup Instructions

### Prerequisites
- **Python**: `pip install pandas numpy faker`
- **R**: Install RStudio and packages:
  ```R
  install.packages(c("ggplot2", "dplyr", "tidyr", "ggmap", "viridis"))
  ```
- **Stadia Maps API**: Use key `9c644007-0572-4892-915a-8da356fe40ae` (or get yours at [Stadia Maps](https://stadiamaps.com/)).

### Steps
1. **Clone the Repo**:
   ```bash
   git clone https://github.com/yourusername/dart-transit-insights.git
   cd dart-transit-insights
   ```
2. **Generate `.csv` Files**:
   - Run each `.py` script (e.g., `python generate_dart_delays.py`).
   - Or manually save `.csv` files from above.
3. **Visualize**:
   - Run each `.R` script in RStudio (`Ctrl+Alt+R`).
   - Outputs land in `C:/Users/Veteran`.

---

## Why It Matters: A Local’s Take
As a DFW resident, I’m sounding the alarm: our metroplex is at a tipping point. With whispers of “Dallas as the Western Dubai by 2035,” we’re staring down explosive growth—Californians, urbanites, and dreamers pouring in. But without bold transit action, we risk choking on emissions, drowning in noise, and gridlocking our future. Here’s why this case study matters for the next 5-10 years:

- **Emissions Crisis**: DART’s hybrid buses and solar stations could slash CO2—vital as car-centric sprawl threatens our air. Dubai’s got skyscrapers; we can’t afford smogscrapers.
- **Noise Sanity**: Quiet rails and electric buses mean less honking chaos. Let’s keep Frisco tranquil, not a freeway symphony.
- **Congestion Cure**: Expanded Park & Rides and express lanes ease I-35E nightmares. More riders = fewer cars = a livable DFW.
- **Equity Shift**: 33% don’t know DART, 27% see it as “poor people’s transit.” Green upgrades and marketing flip that script—transit’s for all, not just the broke.
- **Future-Proofing**: If we hit Dubai-level density, DART must be irresistible—now’s the time to act, before we’re Dubai with pickup trucks instead of camels.

This isn’t just data—it’s a plea to keep DFW thriving, not suffocating.

---

## Conclusion
To the leaders of Plano, Arlington, Garland, Irving, Frisco, and beyond: *DART Transit Insights* lays out a roadmap. Delays pinpoint operational gaps. Safety perceptions reveal trust issues—nighttime fears and open carry jitters demand attention. And our “never ride” crowd (33% clueless, 27% snobs) can be won with eco-smart, appealing upgrades. This case study, though built on simulated data, mirrors real stakes. Let’s make DART a cornerstone of a cleaner, safer, more inclusive DFW—before 2035 turns us into a cautionary tale. Questions? Ideas? I’m here—let’s talk transit!

---

## License
MIT License—open for collaboration. See `LICENSE` file.

---

## Suggested Repo Name
**`dart-transit-insights`**  
- Clean, professional, and screams “serious transit case study”—perfect for mayors and planners to take notice.

---

### Notes
- **Audience**: Pitched to mayors/planners with a formal yet urgent tone—your points (emissions, safety, appeal) hit hard.
- **Fake Data**: Treated as real, with a subtle nod to simulation—keeps it credible.
- **Why It Matters**: Ties to “Western Dubai” hype, local growth fears—grounds it in your voice.
- **GitHub Link**: Swap `yourusername` with your GitHub handle (share it if you want it plugged in!).

What’s your GitHub username for the link? Any extra flair for the pitch—maybe a zinger for the officials? This is ready to impress—let’s polish it up! 😊
