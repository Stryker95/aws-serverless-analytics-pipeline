# AWS Serverless Analytics Pipeline ☁️

![AWS](https://img.shields.io/badge/AWS-Cloud-orange)
![Python](https://img.shields.io/badge/SQL-Analytics-blue)
![Status](https://img.shields.io/badge/Status-Complete-success)

## 🎯 Project Overview

Built a fully serverless data analytics pipeline on AWS to analyze e-commerce sales data. This project demonstrates proficiency in AWS cloud services, SQL analytics, and modern data engineering practices without managing any infrastructure.

## 🏗️ Architecture
```
┌─────────────┐
│   CSV Data  │
└──────┬──────┘
       │
       ▼
┌─────────────────────┐
│   S3 Data Lake      │  ← Raw storage
│  (Object Storage)   │
└──────┬──────────────┘
       │
       ▼
┌─────────────────────┐
│   Glue Crawler      │  ← Auto schema discovery
│  (Data Catalog)     │
└──────┬──────────────┘
       │
       ├──────────────────┐
       ▼                  ▼
┌─────────────┐    ┌──────────────────┐
│   Athena    │    │ Redshift         │
│ (SQL Queries)│    │ (Data Warehouse) │
└─────────────┘    └──────────────────┘
```

## 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| **AWS S3** | Scalable object storage for data lake |
| **AWS Glue** | Automated schema discovery and cataloging |
| **AWS Athena** | Serverless SQL query engine |
| **AWS Redshift Serverless** | Cloud data warehouse |
| **SQL** | Data analysis and transformations |

## 📊 Dataset

E-commerce sales data containing:
- **15 orders** across 4 regions (North, South, East, West)
- **Product information:** Laptops, Monitors, Keyboards, Mice, etc.
- **Customer details:** Names and locations
- **Sales metrics:** Quantity, price, order dates

**Sample Data Structure:**
```
order_id | customer_name | product  | quantity | price  | order_date | region | city
---------|---------------|----------|----------|--------|------------|--------|----------
1        | Rahul Kumar   | Laptop   | 1        | 45000  | 2024-01-15 | North  | Delhi
2        | Priya Singh   | Mouse    | 2        | 500    | 2024-01-16 | South  | Bangalore
...
```

## 🚀 Implementation Steps

### 1. Data Lake Setup (S3)
- Created S3 bucket: `sanchit-sales-data-lake` in Mumbai region (ap-south-1)
- Uploaded CSV sales data to S3
- Configured bucket policies and encryption (SSE-S3)
- Organized data in structured folder hierarchy

### 2. Schema Discovery (Glue)
- Created Glue Database: `sales_analytics_db`
- Configured Glue Crawler with IAM role permissions
- Automated schema detection for 9 columns
- Generated Data Catalog table for SQL access
- **Result:** 100% automated - zero manual schema work!

### 3. Ad-hoc SQL Analysis (Athena)
- Configured Athena query results location in S3
- Executed analytical SQL queries:
  - ✅ Total sales by region
  - ✅ Top-selling products analysis
  - ✅ City-wise performance metrics
  - ✅ Daily sales trends
  - ✅ Average order value calculations

### 4. Data Warehouse (Redshift Serverless)
- Deployed Redshift Serverless workspace (8 RPU)
- Created sales table with optimized schema
- Loaded sample data for analysis
- Performed complex analytical queries
- **Auto-scaling:** Handled workload without manual intervention

## 📈 Key Results

| Metric | Value |
|--------|-------|
| **Total Orders Processed** | 15 |
| **Regions Analyzed** | 4 (North, South, East, West) |
| **Top Region by Revenue** | North (₹184,000) |
| **Most Ordered Product** | Laptop (6 orders) |
| **Query Performance** | <2 seconds (Athena) |
| **Data Scanned per Query** | ~1 KB (extremely optimized) |
| **Project Cost** | ₹0 (100% free tier) |

## 💡 Key Learnings

### 1. S3 as Data Lake Foundation
- **Scalability:** Store unlimited data, pay only for what you use
- **Durability:** 99.999999999% (11 nines) data durability
- **Integration:** Seamlessly connects with all AWS analytics services
- **Cost-effective:** Cheapest storage option ($0.023/GB/month)

### 2. Glue for Automation
- **Zero manual effort:** Crawler auto-detects schema changes
- **Metadata management:** Centralized Data Catalog
- **Time savings:** Eliminates manual schema definition work
- **Keeps in sync:** Automatically updates when data structure changes

### 3. Athena for Quick Analysis
- **No infrastructure:** Query S3 data directly with SQL
- **Pay-per-query:** $5 per TB scanned (first 10 GB/month free)
- **Standard SQL:** Easy to learn, works like PostgreSQL
- **Perfect for:** Ad-hoc analysis, data exploration, quick insights

### 4. Redshift for Production Workloads
- **Columnar storage:** 3-10x faster than row-based databases
- **Serverless mode:** No cluster management overhead
- **Auto-scaling:** Adapts to workload automatically
- **BI integration:** Works with Tableau, Power BI, Looker

## 🎓 Skills Demonstrated

✅ **Cloud Architecture Design** - Designed serverless data pipeline  
✅ **AWS Services Expertise** - S3, Glue, Athena, Redshift  
✅ **SQL Analytics** - Complex aggregations, joins, window functions  
✅ **Data Cataloging** - Metadata management and schema evolution  
✅ **Cost Optimization** - Stayed within free tier limits  
✅ **Serverless Computing** - Zero infrastructure management  
✅ **ETL Concepts** - Extract, Transform, Load patterns  

## 📸 Screenshots

### S3 Data Lake
![S3 Bucket](screenshots/s3-bucket.png)

### Glue Data Catalog
![Glue Catalog](screenshots/glue-catalog.png)

### Athena Query Results
![Athena Query](screenshots/athena-query.png)

### Redshift Analysis
![Redshift Query](screenshots/redshift-query.png)

## 🔧 Sample Queries

**Regional Revenue Analysis:**
```sql
SELECT 
    region,
    COUNT(*) as total_orders,
    SUM(quantity * price) as total_revenue,
    ROUND(AVG(quantity * price), 2) as avg_order_value
FROM sales_data
GROUP BY region
ORDER BY total_revenue DESC;
```

**Top Products:**
```sql
SELECT 
    product,
    SUM(quantity) as total_units_sold,
    SUM(quantity * price) as revenue
FROM sales_data
GROUP BY product
ORDER BY revenue DESC
LIMIT 5;
```

## 💰 Cost Breakdown

| Service | Usage | Cost |
|---------|-------|------|
| S3 Storage | 1 KB | $0.00 (Free tier: 5 GB) |
| Glue Crawler | 1 run | $0.00 (Free tier: 1M objects) |
| Glue Catalog | 1 table | $0.00 (Free tier: 1M objects) |
| Athena Queries | ~5 KB scanned | $0.00 (Free tier: 10 GB/month) |
| Redshift Serverless | Deleted after demo | $0.00 (Free tier: 500 RPU-hours) |
| **TOTAL** | | **₹0.00** 🎉 |

## 🚀 Future Enhancements

- [ ] Implement incremental data loading using Glue Jobs
- [ ] Add data quality checks and validation rules
- [ ] Create Glue ETL job for data transformations
- [ ] Build QuickSight dashboard for visualization
- [ ] Set up CloudWatch monitoring and alerts
- [ ] Implement data partitioning for better performance
- [ ] Add Lambda functions for real-time processing

## 🔗 Connect with Me

- **LinkedIn:** [linkedin.com/in/sanchit-data-engineer](https://linkedin.com/in/sanchit-data-engineer)
- **GitHub:** [github.com/Stryker95](https://github.com/Stryker95)
- **Email:** sanchitpalsingh@gmail.com

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Built with ☁️ by Sanchit Pal Singh**

*Last Updated: February 2026*
