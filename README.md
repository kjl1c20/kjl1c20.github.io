# Data & Analytics Engineering Portfolio
A showcase of key projects delivered during my tenure at Dynamon as a Analytics Engineer, covering data pipeline design, financial modelling, and performance optimisation.


## Emissions Data Quality & Transformation Pipeline
### Problem
Emissions modelling relied on multiple raw data sources with inconsistent formats and varying data quality. In addition, key inputs such as UK government CO₂ emission factors are updated annually, requiring a reliable system to track changes over time. Some values were also based on fixed assumptions, but there was no consistent way to document when these were last reviewed or what sources they originated from. As a result, the lack of clear data lineage and auditability reduced trust in model outputs and made it difficult to trace and diagnose errors in downstream calculations.

### Key Work
- Transformed fragmented reference data into a governed schema by modelling emission factors with explicit scopes, units, and in-row provenance (source, year, notes) within a versioned metadata table.
- Ensured all downstream SQL outputs were fully traceable and explainable by creating a single source of truth, exposed via a read-only view representing the latest approved factor set.
- Enforced data quality at write time using CHECK constraints, a partial unique index, and an active flag to guarantee only one valid version of each factor exists 
- Implemented append-only versioning using a BEFORE INSERT trigger to retire previously active records and maintain a complete audit history of changes.
- Improved reliability of downstream calculations by preventing invalid or duplicate data from entering the system and enabling efficient error tracing.

### Impact
- Improved trust in emission calculation outputs for consultants and clients.
- Enabled faster error tracing by distinguishing between calculation errors and source data issues.
- Created a more reliable and scalable data foundation.

## Total Cost of Ownership (TCO) Data Model
### Problem
Clients required a comprehensive Total Cost of Ownership (TCO) analysis to assess the financial feasibility of transitioning from internal combustion engine (ICE) vehicles to electric vehicles. This involved integrating multiple cost components, including vehicle and charging infrastructure costs, into a single model. The key challenge was to design a scalable data model that could accommodate new cost factors without significant schema changes, while maintaining fast runtime performance to support quick, user-driven recalculations.

### Key Work
- Translated complex business requirements into structured data transformations and model design.
- Built a scalable data model to store and organise cost inputs across vehicle and infrastructure components.
- Designed an Entity Relationship Diagram (ERD) to model relationships between existing datasets and newly introduced cost input and output tables, ensuring a scalable and well-structured schema.
- Developed an incremental dbt model to aggregate TCO at the vehicle level and combine it with vehicle specification data for reporting.
- Designed the model to support extensibility, allowing new cost variables to be added with minimal changes.
- Built and deployed a Python-based calculation engine as an AWS Lambda function, optimising performance to reduce latency and improve responsiveness for user-driven calculations.
- Collaborated closely with stakeholders to refine requirements and present outputs in a format suitable for reporting and decision-making.

### Impact
- Enabled stakeholders to make data-driven financial decisions when evaluating the transition from ICE to electric vehicles.
- Bridged the gap between technical data modelling and business insight by delivering clear, accessible outputs for non-technical users.
### Example Visualisation
<p align="center">Table: Total cost breakdown for current vs All EV Replacement scenario.</p>
<img width="2048" height="573" alt="-" src="https://github.com/user-attachments/assets/69dfcb6c-a2d5-424b-82dd-7a4946e19142" />

<br>

<img width="2048" height="635" alt="unknown" src="https://github.com/user-attachments/assets/d4555910-336b-47b0-8884-454bb914f9af" />
<p align="center"><em>Figure: Charging cost per kWh of on-site charging and public charging.</em></p>

<br>

The visualisation above compares the cost-effectiveness of investing in depot charging infrastructure versus relying on public charging stations. It highlights the difference in cost per kWh between the two approaches, helping stakeholders assess the most financially viable option. The analysis is based on energy consumption data derived from vehicle telematics, ensuring that the comparison reflects real-world usage patterns.

## DBT Optimisation
### Problem
Product merges were taking a significant amount of time due to full dbt refreshes on large tables containing high data volumes. This process often had to be run after hours, consuming considerable developer time and slowing down delivery workflows. Improving the performance of dbt models was necessary to reduce runtime and make the process more efficient and scalable.

### Key Work
- Analysed dbt model performance using EXPLAIN ANALYSE to identify query bottlenecks.
- Optimised SQL logic by removing unnecessary window functions and simplifying transformations.
- Refactored CTEs to improve logical flow and reduce the volume of data processed during joins with large tables.
- Reduced data scanned by restructuring queries to filter earlier in the transformation process.
- Implemented indexing strategies on key dbt tables to improve query performance and join efficiency.

### Impact
- Reduced dbt model runtime, enabling faster and more efficient product merges.
- Decreased manual developer effort required for after-hours processing.
- Improved overall performance and scalability of the data transformation layer.

