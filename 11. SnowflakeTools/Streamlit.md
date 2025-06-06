# Streamlit in Snowflake

## Overview
Streamlit in Snowflake (SiS) allows you to build and deploy data applications directly within Snowflake, eliminating the need for separate infrastructure or complex deployment processes.

## Key Features

### 1. Native Integration
- **Direct Access**: Apps run within Snowflake's security perimeter
- **No Data Movement**: Query data directly without exports
- **Unified Platform**: Build, deploy, and share in one place

### 2. Security and Governance
- **Role-Based Access**: Leverages Snowflake's RBAC
- **Data Governance**: Inherits all Snowflake security policies
- **Secure Sharing**: Share apps like any Snowflake object

### 3. Development Environment
- **Built-in Editor**: Write Python code directly in Snowsight
- **Package Management**: Pre-installed popular libraries
- **Version Control**: Automatic versioning of app code

## Creating Streamlit Apps

### Basic Structure
```python
import streamlit as st
import snowflake.snowpark as snowpark

# Get current session
session = snowpark.Session.builder.getOrCreate()

# Streamlit app code
st.title("My Snowflake App")
df = session.sql("SELECT * FROM my_table").to_pandas()
st.dataframe(df)
```

### Key Components
1. **Session Management**: Automatic Snowpark session
2. **Data Access**: Direct SQL queries
3. **Visualization**: Charts, tables, metrics
4. **User Input**: Forms, sliders, selectors

## Deployment and Sharing

### Deployment Steps
1. Create app in Snowsight UI
2. Write/paste code in editor
3. Click "Run" to deploy
4. App gets unique URL

### Sharing Options
- **Direct Share**: Grant access via Snowflake roles
- **Public Apps**: Make available to all users
- **External Share**: Share with other Snowflake accounts

## Best Practices

### Performance
- Cache expensive queries using `@st.cache_data`
- Limit data fetched to what's needed
- Use Snowflake's query optimization

### Security
- Never hardcode credentials
- Use Snowflake's built-in authentication
- Follow principle of least privilege

### User Experience
- Provide clear instructions
- Handle errors gracefully
- Include data refresh options

## Common Use Cases
1. **Dashboards**: Real-time analytics
2. **Data Apps**: Interactive data exploration
3. **ML Models**: Deploy and interact with models
4. **Reports**: Dynamic reporting tools

## Limitations
- Python only (no R support yet)
- Limited to pre-installed packages
- Compute resources tied to warehouse size
- No external API calls (security restriction)

## Exam Tips
- Understand the security model
- Know the difference between Streamlit in Snowflake vs standalone
- Remember it's Python-based
- Focus on integration with Snowflake objects
- Understand sharing mechanisms

## Sample Questions

**Q1**: What programming language is used for Streamlit in Snowflake?
**A**: Python

**Q2**: How are Streamlit apps shared in Snowflake?
**A**: Through Snowflake's role-based access control (RBAC)

**Q3**: Where does a Streamlit app in Snowflake run?
**A**: Within Snowflake's secure environment, using warehouse compute resources

## Additional Resources
- [Snowflake Documentation - Streamlit](https://docs.snowflake.com/en/developer-guide/streamlit/about-streamlit)
- [Streamlit API Reference](https://docs.streamlit.io/library/api-reference)
- Hands-on labs in Snowflake University