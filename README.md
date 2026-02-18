# Taxi Fleet Analytics Dashboard

Power BI dashboard for taxi fleet operations analysis, using Oslo Taxi as a case study. Simulated operational data covering bookings, revenue, vehicle performance, and payment analytics.

## Dashboard Overview

Four-page strategic dashboard built to handle fleet complexity and reduce operational costs.

```
Hjem --> Oversikt --> Kjøretøy --> Omsetning
  |         |            |            |
Landing   KPIs &      Vehicle      Revenue
 Page    Bookings    Performance   Breakdown
```

## Dashboard Pages

### 1. Hjem (Home)
Landing page with Oslo Taxi branding and navigation.

### 2. Oversikt (Overview)

**Key Performance Indicators:**
| Metric | Value |
|--------|-------|
| Total Bookings | 40K |
| Revenue | 22.25M |
| Total Distance | 1.08M km |
| Avg Distance | 24.61 km |
| Lost Bookings | 25K |

**Trip Status Breakdown:**
- Completed trips (Fullførte)
- Cancelled trips (Kansellerte)
- Incomplete trips (Ufullstendige)

**Visualizations:**
- Monthly bookings trend (Month/Quarter toggle)
- Monthly revenue trend
- Revenue by payment method (Vipps: 23M, Taxifix: 13M, Apple Pay: 6M, Credit Card: 5M, Debit Card: 4M)
- Top pickup location: Oslo S (600)
- Top dropoff location: Blindern (592)
- Driver rating: 4.41
- Customer rating: 4.23

### 3. Kjøretøy (Vehicle Performance)

**Fleet Comparison Table:**
| Vehicle Type | Customers | Revenue | Completed | Share |
|--------------|-----------|---------|-----------|-------|
| Go Sedan | 48,542 | 22,248,141 | 39,754 | 100% |
| Go Mini | 44,666 | 18,176,193 | 32,528 | 100% |
| Premier Sedan | 16,827 | 6,275,332 | 11,247 | 100% |
| Mini Van | 13,382 | 5,146,517 | 9,328 | 100% |
| **Total** | **104,114** | **51,846,183** | **92,551** | **100%** |

**Features:**
- Interactive vehicle selector with visual icons
- Monthly trend sparklines per vehicle
- KPIs update dynamically based on vehicle selection

### 4. Omsetning (Revenue)

**Revenue Segmentation:**

By Vehicle Type:
- Go Sedan: 22M
- Go Mini: 18M
- Premier Sedan: 6M
- Mini Van: 5M

By Payment Method:
- Vipps: 2.3M
- Taxifix: 1.3M
- Apple Pay: 0.7M
- Credit Card: 0.5M
- Debit Card: 0.4M

By Customer ID:
- Top customers ranked by trip count (C9069667: 4.3K trips, etc.)

**Time Analysis:**
- Quarterly revenue trend
- Month/Quarter toggle for granularity

## Data Model

Simulated operational dataset with star schema design.

**Fact Table:**
- Trips (booking_id, vehicle_id, driver_id, customer_id, pickup_location, dropoff_location, distance, fare, payment_method, status, timestamp)

**Dimension Tables:**
- Vehicles (vehicle_id, type, model)
- Drivers (driver_id, name, rating)
- Customers (customer_id, rating)
- Locations (location_id, name, zone)
- Calendar (date, month, quarter, year)
- Payment Methods (method_id, name)

## DAX Measures

Key calculated measures:

```dax
Total Bookings = COUNT(Trips[booking_id])
Total Revenue = SUM(Trips[fare])
Lost Bookings = CALCULATE([Total Bookings], Trips[status] IN {"Cancelled", "Incomplete"})
Avg Distance = AVERAGE(Trips[distance])
Completion Rate = DIVIDE([Completed Trips], [Total Bookings], 0)
Driver Rating = AVERAGE(Drivers[rating])
Customer Rating = AVERAGE(Customers[rating])
```

## Features

**Operational Intelligence:**
- Real-time KPI monitoring
- Lost booking tracking for revenue recovery
- Vehicle utilization comparison
- Payment method optimization insights

**Fleet Management:**
- Vehicle-level performance drill-down
- Revenue per vehicle type analysis
- Completion rate tracking
- Monthly trend monitoring per vehicle

**Revenue Analytics:**
- Multi-dimensional revenue segmentation
- Customer value identification
- Payment method distribution
- Quarterly trend analysis

**Design:**
- Clean light theme with Oslo Taxi branding
- Interactive vehicle selector with illustrations
- Consistent navigation across pages
- Month/Quarter toggle for time analysis

## Technical Stack

| Component | Technology |
|-----------|------------|
| Visualization | Power BI Desktop |
| Data Modeling | Star Schema |
| Calculations | DAX |
| Data Source | Simulated CSV dataset |

## Use Cases

- Fleet managers identifying top-performing vehicles
- Operations teams tracking lost bookings
- Finance teams analyzing payment method trends
- Strategy teams optimizing vehicle allocation
- Customer success tracking high-value customers

## Author

Kesara Rathnasiri
