# Tyree Manufacturing Dashboard

A comprehensive Power BI dashboard analyzing manufacturing operations for Tyree Transformers, tracking production efficiency, quality metrics, and operational bottlenecks across three manufacturing workshops.

## Project Overview

This project demonstrates end-to-end business intelligence development, from database design to interactive dashboard creation. The dashboard provides real-time insights into transformer manufacturing operations, helping identify bottlenecks and optimize production efficiency.

## Dashboard Pages

### Page 1: Production Overview
![Production Overview](screenshots/PAGE_1.png)

**Key Metrics:**
- Production Efficiency: 91.75%
- Defect Rate: 6.55%
- Capacity Utilization: 7.94K units
- On-Time Delivery: 44.40%

**Insights:**
- BESS (Battery Energy Storage Systems) represents the largest production volume
- BESS Production Line leads in total output across all workshops
- On-time delivery performance indicates significant room for improvement

### Page 2: Quality Metrics
![Quality Metrics](screenshots/PAGE_2.png)

**Key Metrics:**
- Average Rework Hours: 1.65 hours
- Defect Rate: 6.55%

**Insights:**
- Majority of products pass quality inspection
- Most common defects: Insulation issues, winding problems, and oil leaks
- Quality trends show variation over the production period

### Page 3: Capacity & Bottlenecks
![Capacity & Bottlenecks](screenshots/PAGE_3.png)

**Insights:**
- Equipment Downtime is the primary bottleneck (~200 delay hours)
- Quality Issues and Material Shortages are secondary concerns
- BESS Production Line has the highest capacity among workshops
- Average productivity: 32.07 units per employee

## Technologies Used

- **SQL Server 2022 Express** - Database management and data storage
- **SQL** - Database schema design and data generation
- **Power BI Desktop** - Dashboard development and visualization
- **DAX** - Calculated measures and metrics

## Project Structure
```
tyree-manufacturing-dashboard/
├── README.md
├── data/
│   ├── schema.sql              # Database table definitions
│   └── sample_data.sql         # Mock production data inserts
├── powerbi/
│   └── Tyree_Manufacturing_Dashboard.pbix
└── screenshots/
    ├── PAGE_1.png              # Production Overview
    ├── PAGE_2.png              # Quality Metrics
    └── PAGE_3.png              # Capacity & Bottlenecks
```

## Key DAX Measures
```dax
Production_Efficiency = 
DIVIDE(
    SUM(Daily_Production[UnitsProduced]),
    SUM(Daily_Production[PlannedUnits]),
    0
) * 100

Defect_Rate = 
DIVIDE(
    SUM(Daily_Production[UnitsRejected]),
    SUM(Daily_Production[UnitsProduced]) + SUM(Daily_Production[UnitsRejected]),
    0
) * 100

OnTime_Delivery_Pct = 
DIVIDE(
    CALCULATE(
        COUNT(Production_Orders[OrderID]),
        Production_Orders[ActualCompletionDate] <= Production_Orders[ScheduledCompletionDate]
    ),
    COUNT(Production_Orders[OrderID]),
    0
) * 100
```

## Database Schema

The project uses 5 main tables:

1. **Production_Orders** - Customer orders and delivery tracking (250 records)
2. **Daily_Production** - Daily output by workshop (260 records)
3. **Quality_Metrics** - Inspection results and defects (100 records)
4. **Workshop_Capacity** - Workshop specifications (3 records)
5. **Production_Bottlenecks** - Operational delays and issues (40 records)

## How to Use

1. **Prerequisites:**
   - SQL Server 2022 Express or higher
   - Power BI Desktop (free version)

2. **Setup Database:**
```sql
   -- Run in SQL Server Management Studio
   CREATE DATABASE Tyree_Manufacturing;
   -- Execute schema.sql
   -- Execute sample_data.sql
```

3. **Open Dashboard:**
   - Open `Tyree_Manufacturing_Dashboard.pbix` in Power BI Desktop
   - Update data source connection to your local SQL Server instance
   - Refresh data

## Business Recommendations

Based on the dashboard analysis:

1. **Address On-Time Delivery** - 44.4% delivery rate requires investigation into scheduling and production planning
2. **Reduce Equipment Downtime** - Implement preventive maintenance to address the primary bottleneck
3. **Optimize BESS Production** - High demand suggests potential for capacity expansion
4. **Quality Control** - Focus on reducing insulation defects and winding issues

## Author

**Hermanto** - [GitHub](https://github.com/IamHermanto)

## License

This project is for portfolio demonstration purposes.

---

*Note: All data in this dashboard is synthetically generated for demonstration purposes and does not represent real manufacturing operations.*